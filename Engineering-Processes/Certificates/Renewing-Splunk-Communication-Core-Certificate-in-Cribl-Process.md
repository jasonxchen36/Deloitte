This process describes how to renew the Splunk Communication Core Certificate that is used for communications between Splunk and Cribl Workers referenced in the Cribl inputs/sources and outputs/destinations.

Follow the instructions below and each worker group with the renewed Splunk Communication Core Certificate.
1. Navigate to the Group Settings:
Worker Groups > [Name of Worker Group] > Group Settings:
![image.png](/.attachments/image-aa18b464-a8b7-406b-9660-ca15ac29c53b.png)
2. Click on the certificate and update the following details:
- Certificate
- Private Key
- Passphrase
- CA Certificate
![image.png](/.attachments/image-af562d33-eb65-4846-9841-b24f303f7728.png)
**Note:** The "Certificate" is the full pem file found in Splunk and can contain the private key. The "CA Certificate" is the chain pem file.
3. Click save and validate the expiry date has been updated:
![image.png](/.attachments/image-3deeb57a-12db-43a8-baeb-d5f9b3e13a7b.png)
4. Commit and Deploy the changes


**Note:** Instead of overwriting the current certificate file you can also make a new certificate and manually switch over the inputs/sources and outputs/destinations (shown by the references in the screenshot below).
![image.png](/.attachments/image-d37d620d-4035-4ca4-8b36-3b120de2e07b.png)

inputs/sources:
![image.png](/.attachments/image-df3f30cc-9102-41a6-b7a5-d28302f9e7be.png)

outputs/destinations:
![image.png](/.attachments/image-f1c6e4b4-0e5f-400d-a1f7-f5da6363c666.png)
