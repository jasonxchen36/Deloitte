# AWS Access Key Rotation for Splunk Service Account

The Splunk Service account access key needs to be rotated after every 90 days. The access key is configured in the Splunk add-on for AWS and is used by the add-on to authenticate to the AWS account every time the add-on makes an API call to AWS for the ingestion of logs. Please see below the steps to rotate the access keys:
1. Remove one heavy forwarder from deployment server management by changing the name of deploymentclient.conf file to deploymentclient.bak on the HF.
2. Sign in to the AWS account and create new access keys for the Splunk service account. The access key for the service account can be created through:
**app1436-prod-splunkreadonlyuser**
IAM --> User --> Splunk user --> app1436-prod-splunkreadonlyuser --> Security Credentials --> Create access key --> Third-party service --> Description tag: Third-party service.
**app1436-prod-splunkglobalironport**
IAM --> User --> Splunk user --> app1436-prod-splunkglobalironport --> Security Credentials --> Create access key --> Application running outside AWS --> Description tag: Application running outside AWS.
The secret access key can only be viewed one time when it is generated, so make sure to save it in a secure place.
3. Update the keys in the designated Heavy Forwarder through the GUI. Make sure to change the access keys (access key and secret access key) in the Splunk add-on for AWS.
![image.png](/.attachments/image-013b789f-3701-4854-8a69-b9acdeeb697e.png)
![image.png](/.attachments/image-eb4d1ee3-52e3-4704-8212-e51d9819b3da.png)
4. Make sure that the changes are reflected in passwords.conf for Splunk add-on for AWS. These changes need to be reviewed on the backend of the HF by accessing via SSH.
![image.png](/.attachments/image-d449ce43-4a53-4ba5-b667-51c30676fa82.png)
5. Search for the CloudTrail logs, S3 access logs, Config logs and VPC Flow logs on the Search Head and make sure logs are coming in from the designated Heavy Forwarder.
6. Copy the changed config files (passwords.conf for Splunk add-on for AWS) back to the Deployment Server.
7. Restore Deployment Server management for the designated Heavy Forwarder by making change to the deploymentclient.conf.
8. Deploy the modified add-ons to all the Heavy Forwarders from the Deployment Server.
9. Inactivate the old keys
10. Test if everything is working fine and the logs are getting ingested through all the Heavy Forwarders
11. If yes, delete the old keys and store the new keys on _Thycotic_.
12. If no, activate old keys again and figure out which Splunk source you are missing

## **app1436-prod-splunkglobalironport**

For this Access and secret key we will have to share with the team that ingests into **index=email_cisco_esa_all**.
Therefore the two values must be uploaded to Thycotic: app1436-prod-splunkglobalironport.

For **EMEA, APAC and AMER (MX and CA)** access and secret key we have to open a ticket:
https://deloitteglobal.service-now.com/sp?id=sc_cat_item&sys_id=28aa62bf379166c03986886643990efc 
POC: Kumar, Anil <anilykumar@deloitte.co.uk>

Example:
https://deloitteglobal.service-now.com/sp?id=ticket&table=sc_req_item&sys_id=083c818287d5e2d0381198ebbbbb3512

For **AMER US** cluster we will need to send an email:
Meds@deloitte.com and GTSCTOEMAILSERVICES@DELOITTE.com

When they update the keys on their side we have to make sure we are getting logs into S3 buckets amer/emea/apac-splunk-global-ironport.

For AWS DCS SYS3 account:

This account is not being handled by us, therefore we need to open a ticket to DCS team: https://deloitteglobal.service-now.com/sp?id=sc_cat_item&sys_id=b56a03c9dbd9ffcccb86d18c689619bc

Fill this form with anything related with AWS.
1. Please select your service under AWS: Create IAM User and Access Keys
2. AWS Account ID: 129567282872
3. AWS Account Name: AWS-DCS-SYS3
4. Permissions: The same as for Splunk-IronPort
5. For any request regarding a person: Dimitri Apostola <dapostola@deloitte.com> or Srinivas Sainathan <ssainathan@deloitte.com>

Please see the table below for the information regarding the service accounts and roles used for each AWS Platform Log Ingestion:
| **AWS Data Source** | **Service Account (User ARN)** | **AWS IAM Role** | **Comments** |
|--|--|--|--|
| MF CloudTrail Logs | arn:aws:iam::129567282872:user/Splunk-ReadOnly-User | arn:aws:iam::129567282872:role/Splunk-ReadOnly-Role |  |
| Legacy CloudTrail Logs | arn:aws:iam::420924285556:user/Splunk-ReadOnly-User  | arn:aws:iam::420924285556:role/Splunk-ReadOnly-Role |  |
| S3 Access Logs | arn:aws:iam::420924285556:user/Splunk-ReadOnly-User | arn:aws:iam::420924285556:role/Splunk-ReadOnly-Role |   |
| Config Logs | arn:aws:iam::129567282872:user/Splunk-ReadOnly-User  | arn:aws:iam::311648320290:role/splunk_ops_assume_role | The Splunk user within CEM account assumes the IAM role within the Global Ops account owned by DCS |
| VPC Flow Logs | arn:aws:iam::420924285556:user/Splunk-ReadOnly-User   | arn:aws:iam::420924285556:role/Splunk-ReadOnly-Role |  |
