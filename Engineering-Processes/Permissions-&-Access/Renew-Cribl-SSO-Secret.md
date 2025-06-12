The purpose of this document is to explain how to update the secret to the Azure Apps used for Cribl Single Sign On (SSO) authentication.

**Dev**
Name:  DTTL App1436 Cribl Portal EMEA NONPROD
Client ID: d4f767c8-fcdf-4a18-a599-a0f01bba1445
IAM URL: https://appreg.iam.deloitteresources.com/AppSecrets/d4f767c8-fcdf-4a18-a599-a0f01bba1445

**Prod**
Name:  DTTL App1436 Cribl Portal EMEA PROD
Client ID:  85703ec1-b9fe-4665-b7f4-56aafe57e612
IAM URL: https://appreg.iam.deloitteresources.com/AppSecrets/85703ec1-b9fe-4665-b7f4-56aafe57e612

1. Generate a new secret on the IAM website and update the new secret in Thycotic
2. Login to Cribl and navigate to **Settings** > **Global** > **Access Management** > **Authentication**
![image.png](/.attachments/image-b67af14a-ae97-4797-b16e-58112e49e60c.png)
3. Update the **Client secret** and click on **Save**
4. The Cribl leader will reboot. Logout and validate the SSO authentication works when logging in with your a-account.
