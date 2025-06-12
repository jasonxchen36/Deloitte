WIP
**Introduction**
The main subject of this article is explain how to renew the SAML token/secret in AZURE and then deploy to SH Adhoc and ES.

For example:
**ALERT** AzureAD app credentials nearing expiration [DTTL App1436 Splunk EMEA Cloud ES NONPROD]
![image.png](/.attachments/image-728023e3-dd46-4ed0-a627-9972715714f5.png)

For each region APAC and EMEA we have four token. Two for Adhoc SH, Prod and NonProd (dt-region.splunkcloud.com) and two for ES SH, Prod and NonProd (es-dt-region.splunkcloud.com).

**Steps**
We have to create a new secret in appreg.iam.deloitteresources.com. We can have both old and new secrets at the same time in case we need to roll back.
![image.png](/.attachments/image-f287c424-b4ab-426e-aaf6-177b896106ec.png)
Once it is created we will copy the secret given and put it in the SH needed:
![image.png](/.attachments/image-26cf880d-0d7d-45e2-91bd-33c260ad73d5.png)
In authentication Methods go to Configure Splunk to use SAML
![image.png](/.attachments/image-b65f30a2-166b-41f8-88f6-2154434136bd.png)
![image.png](/.attachments/image-a7a8b422-a13f-4491-accb-3b143046d14e.png)
Once we are at the configuration pop up we will update only clientSecret value with the new one given by the appreg.
![image.png](/.attachments/image-4d201ca6-7848-42f0-bbd6-c88a220e3aef.png)

Once this is done we will update the new secret into Thycotic/PCS:
![image.png](/.attachments/image-df2f3f09-ac76-4954-b501-88037fd8f971.png)