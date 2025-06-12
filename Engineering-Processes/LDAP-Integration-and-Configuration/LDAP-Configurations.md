As it is stated in the previous Wiki Article, the configuration for both AMER and EMEA Cloud will be present in az1436l035 until APAC is merged as well, in the meantime APAC's configuration regarding LDAP will be present in aw1436l036.

In opt/splunk/etc/apps there's an application named **SA-ldapsearch** that contains all configurations, also, another application named **del_prod_ldap_route** that makes sure the data is being routed into Cloud SH's:

**outputs.conf:**

![image.png](/.attachments/image-45003747-c3a7-4630-bb6f-41521bd28900.png)

Note: You can see the APAC VIP here since the EMEA one is already present in SA-ldapsearch app by default, since it is in the EMEA region.

**transforms.conf:**

![image.png](/.attachments/image-9c0de57c-7547-4824-a1f1-865b0a0d29f2.png)

TCP Routing configuration.

**props.conf:**

![image.png](/.attachments/image-4190448d-183f-48fe-8f2f-a55bc96022b9.png)

Note: We specify the routing for the ldapsearch sourcetype, reason begin that, when we run the query, we use summary_index functions as we can see here in the SA-ldapsearch app:

![image.png](/.attachments/image-4b578d07-2996-4638-8f11-0fa1e0623694.png)

And we cannot edit the sourcetype by default (stash) with these summary_index configurations, that why we specify the sourcetype on the other app.


Some last info regarding LDAP, the only index containing ldap events is **referential_ldap_identity_all**.

_All this configuration and changes made into the Saved Searches was done by Jhonny Coca._

