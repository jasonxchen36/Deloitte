
# **Overview:**
The Azure Build Guide details the different steps required to deploy the Azure Cloud Splunk Monitoring Environment.

## **Azure Build Guide Contents:**
1. Azure Subscription Requisition

2. Azure Resource Group Creation
3. Virtual Network and Route Table Creation - [DCS Connected - VPC/VNET Request](https://deloitteglobal.service-now.com/sp?id=sc_cat_item&sys_id=35e69db3dbc0b3c47379e0a1ca96195d) 
4. Network Security Groups Creation
5. Subnets Creation
6. Load Balancers Creation
7. VNET Peering Implementation
8. Firewall Policy Requests - [Firewall Policy Change Requests](https://deloitteglobal.service-now.com/sp?id=sc_cat_item&sys_id=47088b21378b360031119c9953990e41)
9. Virtual Machines Creation - [Azure Virtual Machine Server Build Request](https://deloitteglobal.service-now.com/sp?id=sc_cat_item&sys_id=23333976db797b40d6ee6def4b9619ab) 
10. Splunk Installation and Configuration Changes - Run install script
11. SAML EntityId Requests
12. DNS Implementation - [DNS and WINS Request](https://deloitteglobal.service-now.com/sp?id=sc_cat_item&sys_id=ff71c47337d6268431119c9953990e5d)
13. Splunk Web Certificate Implementation
14. DevOps Integration
16. Thycotic Integration



---
# **Azure Subscription Requisition:**

Submit a Cloud Provision Request through the OneCloud portal and the Deloitte Cloud Services Operations team will create an Azure subscription.

Example of completed request(s):
- INC1277923

Include the following information within the request:


| Tag Name     | Description                                                                                                                                                                                                                                            | Value                                                                                                              |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| MEMBER FIRM  | Two to five-character code for your member firm.                                                                                                                                                                                                       | DTTL                                                                                                               |
| COUNTRY      | Two-character country code representing the primary country responsible for account usage and cost reporting.                                                                                                                                          | Global                                                                                                             |
| FUNCTION     | Unit of organization immediately below the member firm level.                                                                                                                                                                                          | GTS                                                                                                                |
| CONTACTS     | JSON formatted values of the most responsible group and person(s) for business and technical management of the resource. This can include the primary architect and/or support engineer(s) of the resource.                                            | “UserId”: “jjoels@deloitte.com”, “UserId”: “jkissell@deloitte.com”, “UserId”: “ddefibaugh@deloitte.com”            |
| BILLING CODE | This is the mechanism used to assign resources to the billing / accounting system. In the US, this is in the form of a WBS code, but could be any form of billing code, engagement number, or other entry deemed appropriate to facilitate chargeback. | DGS00013-01-01-01-1000                                                                                             |
| CS           | JSON Formatted values for data classification for resource based on PM40/Cyber Security standards. This will follow three elements: General Classification, Data Type, Data Qualifier.                                                                 | “GeneralClassification”: “Confidential”, “DateType”: “Deloitte data”, “DataQualifier”: “Personal information (PI)” |

---

# **Azure Resource Group Creation**

To create Resource Groups, the Deloitte Cloud Services Operations team performs the following steps:

1.	Access https://portal.azure.com
2.	Navigate to the Home > Route tables 
3.	Click on Add

![image.png](/.attachments/image-b73080a8-29d1-4479-8f6f-e340d81a2d00.png)

4.	Click on the Basic tab and configure the following settings:

| Setting        | Value                         |
|----------------|-------------------------------|
| Subscription   | US-AZSUB-EMA-ENA-ProjectS-PRD |
| Resource group | AZRG-EUN-ITS-PROJECTS-PRD     |
| Region         | North Europe                  |

5.	Click on Review + Create

---

# **Virtual Network and Route Table Creation**

Submit a VPC/VNET Creation Request in ServiceNow and someone from the Deloitte Cloud Services Network team will create the Virtual Network (VNET).

Example of completed request(s):
•	RITM0261434
•	RITM0261435
•	RITM0265650
•	RITM0265654

To create Virtual Networks, the Deloitte Cloud Services Network team performs the following steps:
1.	Access https://portal.azure.com
2.	Navigate to the Home > Virtual networks 
3.	Click on Add

![image.png](/.attachments/image-465524d2-2520-45a3-8ac5-1acb5494701d.png)

4.	Configure the following settings:

| Setting              | Value                         |
|----------------------|-------------------------------|
| Virtual network name | azeunprdvnet01-ProjectS-PRD   |
| Address space        | 10.222.7.64/26                |
| Subscription         | US-AZSUB-EMA-ENA-ProjectS-PRD |
| Resource group       | AZRG-EUN-ITS-PROJECTS-PRD     |
| Location             | (Europe) North Europe         |
| Subnet name          | ProjectS-Subnet1              |
| Address range        | 10.222.7.16/28                |
| DDoS Protection      | Basic                         |
| Service endpoints    | Disabled                      |
| Firewall             | Disabled                      |

5.	Click on Create

To create Route Tables, the Deloitte Cloud Services Network team performs the following steps:
1.	Access https://portal.azure.com
2.	Navigate to the Home > Route tables 
3.	Click on Add
![image.png](/.attachments/image-0901352a-4199-4c76-a9fc-72913624f140.png)
4.	Configure the following settings:

| Setting                                   | Value                     |
|-------------------------------------------|---------------------------|
| Route table name                          | RT-EUN                    |
| Subscription                              | AZRG-EUW-ENA-ProjectS-DEV |
| Resource group                            | RT-EUN                    |
| Location                                  | (Europe) North Europe     |
| Virtual network gateway route propagation | Enabled                   |
	
5.	Click on Create

---
# **Network Security Groups Creation:**
To create Network Security Groups, the Project S Deployment STORM team performs the following steps: 
1.	Access https://portal.azure.com
2.	Navigate to the Home > Network security groups
3.	Click on Add
 
4.	Configure the following settings:

| Setting        | Value                         |
|----------------|-------------------------------|
| Name           | EUAZUGTS01001-nsg             |
| Subscription   | US-AZSUB-EMA-ENA-ProjectS-PRD |
| Resource group | AZRG-EUN-ITS-PROJECTS-PRD     |
| Location       | (Europe) North Europe         |


5.	Click on Create

---
# **Subnets Creation:**
To create Subnets, the Deloitte Cloud Services Network team performs the following steps:
1.	Access https://portal.azure.com
2.	Navigate to the Home > Virtual networks
3.	Click on azeunprdvnt01-splunk
4.	Click on Subnets
5.	Click on Subnet
 
 
6.	Configure the following settings:

| Setting                    | Region 1         | Region 2         |
|----------------------------|------------------|------------------|
| Name                       | ProjectS-Subnet1 | ProjectS-Subnet2 |
| Address range (CIDR block) |                  |                  |
| Network security group     |                  |                  |
| Route table                |                  |                  |
| Services                   |                  |                  |

7.	Click on OK
