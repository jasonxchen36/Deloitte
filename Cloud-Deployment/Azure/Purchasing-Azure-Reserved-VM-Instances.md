This wiki page describes how to purchase reserved VM instances in Azure environment.

Procurement for the Cloud Environments is set to be run twice-annually.  Once in January and once in July.
Reviews of the environments should be conducted at least one month in advance to determine any net-new infrastructure that might be required to support ingest.

The DTTL ECMS Azure: [DTCMSAzure@deloitte.com](mailto:DTCMSAzure@deloitte.com "mailto:dtcmsazure@deloitte.com") team works on cloud cost efficiencies, and should be consulted to assist in reviewing current infrastructure to help determine if resizing of specific instances should be performed ahead of reservation.

To perform the reservations, either work with the DTTL ECMS Azure team, or perform the following steps:

 
1. Navigate to the Virtual Machine page and click on Purchase from the Reservations drop menu.
![image.png](/.attachments/image-b594a53c-37e6-4b84-a963-490e9b13e032.png)

1. Filter the reserved VM instances and select the virtual machine to purchase and click Add to cart.
**Scope:** Single subscription
**Scope and billing subscription:** DTTL-AZSUB-ALL-PORT008-Azure Splunk-PRD
**Term:** Three Years
**Billing frequency:** Upfront

![image.png](/.attachments/image-87479598-1a4e-4920-a86d-41fe2246f1fa.png)

3. Click on the Advanced settings gear icon and select Capacity priority and click OK
![image.png](/.attachments/image-dc10307f-cfd0-472b-8eac-655147e0d68d.png)
![image.png](/.attachments/image-f87b84ef-8a4f-4a29-8e58-aca00b1e0105.png)

4. Click Next: Review + buy and proceed to purchase the reserved VM instances.

5. After the purchase is complete, DCS will contact you and ask to provide the following information:
- Member Firm
- WBS Code
- Cost Center for Event Monitoring
- Subscription Name
- Subscription ID

**Note:** The user purchasing the reserved VM instances will only have access to view the reservations by default. After the purchase is complete, the user must add the "sg-all splunk all_gems_engineer_azure_admin" group for others to access it by navigating to Reservation > Access control (IAM) > Role assignments and clicking Add.

![image.png](/.attachments/image-8125979d-29fe-4446-83ce-712e96cdf593.png)