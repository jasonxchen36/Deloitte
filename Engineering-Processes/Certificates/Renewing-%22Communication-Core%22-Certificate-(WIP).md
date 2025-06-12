**Renewal process on Venafi**

The following steps below outline how to renew and replace "Communication Core" certificate. This certificate is used for SSL secure communication between Splunk servers.

1. First of all, we have to renew this certificate in Venafi (search certificate by "prodsplunk.atrame.deloitte.com". 

2. Configuration for downloading the renewed certificate:
![image.png](/.attachments/image-0f32207a-978a-4f6a-a2b3-757f0407f324.png)
<IMG  src="https://dev.azure.com/GlobalSOC/93d9ecc1-89fd-4a34-a69b-7282df6fad64/_apis/git/repositories/7c3c331d-0fac-420a-9ad2-1a920f9247d9/Items?path=/.attachments/image-fe9b3fe9-6a11-4ae2-ac21-ed391b76a361.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster"  alt="image.png"/>

**Note**: In this renewed certificate that we have downloaded, we have 4 diferent blocks: the first three corresponding to deloitte, and the last one to the machine itself.

**Note**: If on any occasion, the key used for this certificate is compromised, we must create a new one and a new csr for the certificate.

3.  Generate a new "splunk_prod_cert.pem" with the following order:

ORDER:
- subject=E=dt-cyberdefenseengineering-architecture@deloitte.com, CN=prodsplunk.atrame.deloitte.com, OU=DTS, O=Deloitte, L=Glen Mills, S=PA, C=US
![image.png](/.attachments/image-ceb36db8-eae5-4ac6-8d65-8da957019eff.png)
![image.png](/.attachments/image-40a3f683-1dfd-47f6-900c-8a32c9bdf8f4.png)
- RSA PRIVATE KEY  (You can find it in old certificate)
- subject=E=dt-cyberdefenseengineering-architecture@deloitte.com, CN=prodsplunk.atrame.deloitte.com, OU=DTS, O=Deloitte, L=Glen Mills, S=PA, C=US
- subject=CN=Deloitte SHA2 Level 3 CA 2, DC=atrame, DC=deloitte, DC=com
![image.png](/.attachments/image-a84ee841-a919-49c3-9979-60b060f154bd.png)
![image.png](/.attachments/image-135977c0-b526-4378-bb51-9d994bbb0707.png)
- subject=CN=Deloitte SHA2 Level 2 CA 2, DC=Deloitte, DC=com
- subject=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com

As you can see in the old splunk_prod_cert.pem we have the order but only leave BEGIN/END CERTIFICATE and what is between them, so we delete the strings such as "subject=E=dt-cyberdefenseengineering-architecture@deloitte.com, CN=prodsplunk.atrame.deloitte.com, OU=DTS, O=Deloitte, L=Glen Mills, S=PA, C=US", "subject=CN=Deloitte SHA2 Level 3 CA 2, DC=atrame, DC=deloitte, DC=com", "subject=CN=Deloitte SHA2 Level 2 CA 2, DC=Deloitte, DC=com" and "subject=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com"

4. Generate a new "splunk_prod_chain.pem":

**IMPORTANT**: We have also need to add the chain from dt_emea/apac_cacert.pem on the 100_dt-apac/emea_splunkcloud_* app into splunk_prod_chain.pem and viceversa so splunk_prod_chain.pem and dt_emea/apac_cacert.pem have to be the same.

ORDER:
- subject=CN=Deloitte SHA2 Level 3 CA 2, DC=atrame, DC=deloitte, DC=com
![image.png](/.attachments/image-a84ee841-a919-49c3-9979-60b060f154bd.png)
![image.png](/.attachments/image-135977c0-b526-4378-bb51-9d994bbb0707.png)
- subject=CN=Deloitte SHA2 Level 2 CA 2, DC=Deloitte, DC=com
- subject=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com
- Chain from dt_region_cacert.pem. We should copy it from BEGIN CERTIFICATE to END CERTIFICATE so we have three times each.

As you can see in the old splunk_prod_chain.pem we have the order but only leave BEGIN/END CERTIFICATE and what is between them, so we delete the strings such as "subject=E=dt-cyberdefenseengineering-architecture@deloitte.com, CN=prodsplunk.atrame.deloitte.com, OU=DTS, O=Deloitte, L=Glen Mills, S=PA, C=US", "subject=CN=Deloitte SHA2 Level 3 CA 2, DC=atrame, DC=deloitte, DC=com", "subject=CN=Deloitte SHA2 Level 2 CA 2, DC=Deloitte, DC=com" and "subject=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com"

This is one of the critical processes, since if the certificate is displayed incorrectly, we lose communication between servers. 
Therefore, it is recommended to follow a process to verify that it works correctly.

These two certificates need to be updated on the core apps within Deployment Servers, Heavy Forwarders and Intermedial Forwarders.

We have several environments and regions to update the certificate on:
**EMEA**:
OnPrem, Azure and AWS.
**AMER**:
OnPrem, Azure, AWS, AMER RDC, GPC and I&P ([How to access I&P servers - Overview](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/1034/How-to-access-I-P-servers)).
**APAC**:
Azure and AWS.
**Others**:
CBC Relativity (kydiscoverspl*)

**List of hosts to deploy the certificates**

[Certs_Core_RollOut_planning_2026.xlsx](https://amedeloitte.sharepoint.com/:x:/r/sites/CyberDefenseEngineering/_layouts/15/Doc.aspx?sourcedoc=%7BE2270385-C630-4B9A-B17E-B06554DC61D2%7D&file=Certs_Core_RollOut_planning_2026.xlsx&action=default&mobileredirect=true)

In order to update the certificate we will apply the changes from the Deployment Servers or on the HF itself. The process from the DS is:

**Note**: All these changes need to be done with the splunk service account: dtt_sc_splunk_prd or dtt_sc_splunk_qa.

First of all go to the path of the core app for UF, IF and HF in deployment-apps:
$SPLUNK_HOME/etc/deployment-apps/<core_apps>/auth
core_apps for example for DS AWS AMER:
![image.png](/.attachments/image-eb0146fb-de24-400b-a85c-fa64f830a5e6.png)
Once we are in the app, we will create a backup of the old certificates.
`mv splunk_prod_chain.pem splunk_prod_chain.pem2`
`mv splunk_prod_cert.pem splunk_prod_cert.pem2`
And with vi insert the new certificates with the same name: splunk_prod_chain.pem and splunk_prod_cert.pem.![image.png](/.attachments/image-752d54aa-9896-4857-b941-6f6eda5df204.png)
We can check for the new expiration date for the certificates:
`/opt/splunk/bin/splunk cmd openssl x509 -enddate -noout -in *.pem`
![image.png](/.attachments/image-84947677-05b0-4e26-9453-7600b6836cc1.png)

Once all the core apps are done we would need to update the dt-region_cacert.pem:
$SPLUNK_HOME/etc/deployment-apps/100_dt-region_splunkcloud*/default/
Note: The name of the certificate is set to APAC or EMEA but for AMER region it is set to EMEA:
![image.png](/.attachments/image-ab33b03c-bbe9-4772-af4f-c4e0874563b2.png)

**Note**: If we want to apply the changes for the deployment-apps/<core_apps> without having to update the certificate for the Deployment Server we must reload the server-class for the core apps or 100_dt-region_splunkcloud* app
To know the server-class for any app:
`find $SPLUNK_HOME/etc/ -type f -name "serverclass.conf" | xargs grep -R --colour '<app>'`
To reload the server-class (admin password for the DS needed):
`$SPLUNK_HOME/bin/splunk reload deploy-server -class <server-class name>`

When we finished with the core apps and 100_dt-region_splunkcloud* app we can move on to the core app for the DS itself.

**Note**: This process also applies to HF or IF that we would need to update the certificate manually like: GCP, I&P or CBC Relativity.
$SPLUNK_HOME/etc/apps/del_region_*_communication_core/auth/
![image.png](/.attachments/image-2efbd6ab-066f-4a43-a0e9-e14620f236fa.png)

Once the Deployment Server or HF/IF that need to be updated manually have been updated we will have to restart the service.
`$SPLUNK_HOME/bin/splunk restart`

**Cribl:**

Once it is renewed we need to update it also for Cribl: [Renewing Splunk Communication Core Certificate in Cribl Process - Overview](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/986/Renewing-Splunk-Communication-Core-Certificate-in-Cribl-Process)

We would need to check the internals for the hosts that we made the changes for, also if is the case such as HF/IF doing phone home to the Deployment Servers correctly.
Check for internals. In either APAC or EMEA SHs:
`index=_internal host=<host>`

Server phoning home to DS:
![image.png](/.attachments/image-fff9da6d-6e1d-41fb-8a8b-b4ac16d7e3b4.png)
![image.png](/.attachments/image-e622235e-2b97-4e88-9086-f17287952a9c.png)


WIs related to this task: [Task 138089 Certs renewal for Splunk communication core app - 2023](https://dev.azure.com/GlobalSOC/Splunk/_workitems/edit/138089) [Task 138089 Certs renewal for Splunk communication core app - 2023](https://dev.azure.com/GlobalSOC/Splunk/_workitems/edit/138089) [Task 182742 Certs renewal for Splunk communication core app - 2024](https://dev.azure.com/GlobalSOC/Splunk/_workitems/edit/182742/) and [Task 237631 Certs renewal for Splunk communication core app - 2025](https://dev.azure.com/GlobalSOC/Splunk/_workitems/edit/237631/)

Last but not least, we need to update the core certificate into the Upgrade Splunk Package.
