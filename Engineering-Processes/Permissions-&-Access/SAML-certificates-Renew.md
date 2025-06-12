**Prerequisite**

To activate the new SAML certificate it is mandatory to be at the same time as the created PR is live.

**Introduction**

The main subject of this article is explain how to renew the SAML certificates in AZURE and then deploy to SHC

**Steps**

When a SAML certificate is soon to expire, we will received a mail notification from AZURE with subject **"[EXT] Action required: Renew your application certificate in Azure Active Directory**" or similar:

![image.png](/.attachments/image-447275ce-0718-409b-8f3e-2834628adc93.png)

1. After check the email we need go to [Azure Portal](https://portal.azure.com) 

Go to Azure Active directory/Microsoft Entra ID --> Enterprise Application then filter by name

![image.png](/.attachments/image-b5a58cf8-ffb6-4a62-9173-87510bc866b1.png)

Then select the correct App and copy the Application ID

![image.png](/.attachments/image-5fea4fb8-2c9d-416c-983f-4206e7793a3a.png)

2. If we created/requested the app we can check it here: [list of your registrations](https://appreg.iam.deloitteresources.com/listapps) or we can copy the Application ID here https://appreg.iam.deloitteresources.com/viewappreg?id=XXXXXXXXXXXXXXXX

**NOTE:** If we did not create the App we are not able to view and we can not continue by ownselft, and we need to create a [Service Now ticket](https://deloitteglobal.service-now.com/sp?id=sc_cat_item&sys_id=6591c854db09b4d08c54929cd396198e) to renew and then to activate the certificate.

3. After, we need to create a new certificate from this form:

![EditSaml.png](/.attachments/EditSaml-222e6d77-120f-4ced-8d1d-34ab49814109.png)

4. When the new certificate is created we will download, open with notepad++ or similar editor, copy the certificate, and create a PR/replace for the app **del_AMER/EMEA/APAC_prod_authentication_saml/auth/idpCert.pem**

5. Then we need to restart Splunk or wait to PR will apply to activate the certificate

![ActivateSaml.png](/.attachments/ActivateSaml-c84b310a-b0f9-4d53-a747-433d3b3c7ea6.png)
