The Asset and Identity Framework performs asset and identity correlation for fields that might be present in an event set returned by a search. The Framework relies upon lookups and configurations managed by ES Admins. 

**Thycotic and SNOW CMDB Data** 

Splunk Architecture Team migrated the Thycotic identities lookup gen and the SNOW CMDB lookup gen to the Asset and Identity Framework located in SA-Identity Management. 

**Lookup Names:**
administrative_identity_lookup
deloitte_ldap_identities
secret_server_identity
deloitte_ldap_domain_controllers
deloitte_servicenow_assets
-----
----

_The current Asset and Identity framework used by ES_

Please take the below steps in PROD

1. From the Splunk ES menu Bar, select configure--> Data Enrichment--> Asset and Identity Management 
2. Click New in the top right Corner
3. Select the corresponding transforms.conf in the source drop down list, give it a name, description, and check the Blacklist box in order to exclude from bundle replication
4. click save.

Once you have confirmed the changes are working as planned, please migrate the .confs to production following the procedure above. 

Migrate the lookups and transforms to the SA-Identity-Management App to their respective folder

_IMPORTANT_

1. If anyone want to explicitly use asset and identity framework in their search, please use below macros

`get_identity4events(user)`
`get_asset(src)`


Asset correlation compares events that contain data in any of the src, dest, or dvc fields against the merged asset lists for matching IP address, MAC address, DNS name, or Windows NT host names. Asset correlation no longer occurs automatically against the host or orig_host fields.

Identity correlation compares events that contain data in any of the user or src_user fields against the merged identity lists for a matching identity.

2. Asset and Identity dashboards can access by following path in ES

Asset Center Dashboard: 
  Navigation : Enterprise Security -> Security Domain -> Identity -> Asset Center

Identity Center Dashboard: 
Navigation : Enterprise Security -> Security Domain -> Identity -> Identity Center


------
------
# * Important Thycotic Lookup change- The Owner field has been renamed to managedBy, this change is already reflected in Production and content that leverages this lookup.

_Please refer to the additional links for Splunk Documentation and information _
https://docs.splunk.com/Documentation/ES/6.1.0/Admin/Manageassetsandidentities
https://docs.splunk.com/Documentation/ES/6.1.0/Admin/Formatassetoridentitylist