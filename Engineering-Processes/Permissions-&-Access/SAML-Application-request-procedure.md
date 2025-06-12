# **Introduction** 

Guide to create a new SAML application in Azure to be used in Splunk to enable SSO.

Azure team provided this link to request a new app: https://appreg.iam.deloitteresources.com

Click on _Register New AzureAD Application_ to start the process.

![SAML00.png](/.attachments/SAML00-f20ee85a-cf98-4991-a9d7-2e58ae3de85c.png)

**Note:** This guide is based on the creation of an App called DTTL App1436 **Splunk Portal PRO AMER SHC** PROD.

1. Set the name, the MF and the App Code. 
Choose app porpoise: production or not production environment.
**Note:** MF, App Code and Environment values are added to the final App name as prefix and suffix.

![SAML01.png](/.attachments/SAML01-5c8a6d17-b361-4909-8e4f-1c2efad57c7c.png)

2.  Select "No" to both questions in Step 2 since it not a DPASS application migration and guest access will not be allowed.

![SAML02.png](/.attachments/SAML02-51304349-c336-4712-9830-3474f40d48f8.png)

3. Select "Splunk Enterprise and Splunk Cloud" from Custom Enterprise App

![SAML03.png](/.attachments/SAML03-6ba3eb8d-4b08-4007-83e5-c4b222832bab.png)

4. In this step it's needed to define ID and URL for new our application.
**Note:** SAML Entity ID should be used in the Splunk SAML app.

![SAML04.png](/.attachments/SAML04-8d0cf3ac-8789-4fd8-be7a-b5d0ec7be94e.png)

5. This step is only for verification. I've never faced to "related Application already registered" message.
If you face this, please contact Azure team.

![SAML05.png](/.attachments/SAML05-ba8616db-42ce-4799-8cbd-ae2c59eccbe0.png)

6. Select "Yes" to both questions in Step 6 since MFA and SSO features are required.

![SAML06.png](/.attachments/SAML06-4279bd71-c19b-41da-98d1-298a57c9e57f.png)

7. Make sure Primary Claim Identifier is set as "Windows Account Name" and all the 4 Custom claims are added.

|Name | Value  |
|--|--|
| Unique User Identifier (Name ID) | user.onpremisessamaccountname  |
| http://schemas.microsoft.com/ws/2008/06/identity/claims/role | user.groups [SecurityGroup] |
| mail | user.mail |
| realName | user.displayname |


Advanced Certificate Signing options should be set as shown as well.

**Note:** Notification email could be our email since all notifications will be sent also to Team Email, configured in Step 10.

![SAML07.png](/.attachments/SAML07-2a9c6ddd-fb7f-4fba-8a56-b1e6038ff504.png)

8. Since no Custom App Roles are required, this step should be skipped.

![SAML08.png](/.attachments/SAML08-59aaf7eb-3252-4239-bcfa-09653e73bb87.png)

9. Since no API Permissions are required, this step should be skipped.

![SAML09.png](/.attachments/SAML09-44a30ec1-957c-4999-a986-17cd40b6bff2.png)

10. Add a description for App and make sure email addresses are populated. 

![SAML10.png](/.attachments/SAML10-b7a683c9-7475-4aa7-8e1d-4e25471750ed.png)

11. Click Finish to end the process.

12. Request to Azure Team "Enable max_size_limit for SAML response" is set to true for this new application.
**Note:** Use the following [ServiceNow Template](https://deloitteglobal.service-now.com/sp?id=sc_cat_item&sys_id=6591c854db09b4d08c54929cd396198e)





