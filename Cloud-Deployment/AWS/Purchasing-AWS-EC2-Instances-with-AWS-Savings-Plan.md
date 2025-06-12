Savings Plan is a flexible pricing model offered by AWS that provides savings in the price of AWS EC2 instances in exchange for a commitment to use a specific amount of compute power (measured in $/hour) for a 1 or a 3 year period. DTTL has purchased Savings Plans for the Splunk servers within the 3 Splunk AWS regions – North Virginia, Ireland and Tokyo. The current Savings Plans have been purchased for a term of 1 year. 

Procurement for the Cloud Environments is set to be run twice-annually.  Once in January and once in July.
Reviews of the environments should be conducted at least one month in advance to determine any net-new infrastructure that might be required to support ingest.

The DTTL ECMS AWS: [DTCMSAWS@deloitte.com](mailto:DTCMSAWS@deloitte.com "mailto:dtcmsaws@deloitte.com") team works on cloud cost efficiencies, and should be consulted to assist in reviewing current infrastructure to help determine if resizing of specific instances should be performed ahead of reservation.

To perform the reservations, either work with the DTTL ECMS AWS team, or perform the following steps:

 •	Login to the console of the Project S AWS Account using the following link: https://myapplications.microsoft.com/

•	Click on the “Services” drop down at the top left and select “Billing”

•	Select “Savings Plan” --> “Inventory” and you should be able to view the 3 Savings Plans that have been bought for the AWS EC2 instances in the 3 main Splunk AWS regions (North Virginia, Ireland and Tokyo)

•	The Savings Plan Inventory contains details such as Type, Instance Family, Region, Start Date and End Date. Please refer to the AWS documentation for Savings Plan for more information and reference

•	If any Savings Plan has reached the End Date, you can buy a new Savings Plan to purchase the EC2 instances for that region for 1 year by clicking on  “Purchase a Savings Plan”  and selecting the following options:
Savings Plan Type: EC2 Instance Savings Plan
Term: 1 year
Region: North Virginia/Ireland/Tokyo
Instance Family: C5 (All AWS Splunk servers belong to the C5 EC2 instance family)
Purchase Commitment: Per hour usage according to Savings Plan rate (Refer the current commitment from the Inventory)
Payment Option: All Upfront 

Prior to buying the Savings Plan, it is important to send an approval request to the CEM leadership along with the dollar amount for the Savings Plan.
