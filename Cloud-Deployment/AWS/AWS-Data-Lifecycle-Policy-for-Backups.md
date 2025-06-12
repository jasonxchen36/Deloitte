AWS offers a service called Data Lifecycle Manager that helps in managing the backups of the AWS instances as well as EBS volumes attached to the instances.

Currently, we have 2 policies created and enabled within the AWS Data Lifecycle Manager:

### **EBS-backed AMI policy** 
This type of policy automates the creation, retention, and deletion of EBS-backed AMIs. What that means is that this policy creates an AMI of a VM which contains the snapshots of all the EBS volumes that are attached to a particular VM. We are currently using this policy for taking a back-up of all the Splunk servers except for the Indexers. The reason we are not including the Splunk Indexers as part of this policy is because we do not want to back-up the EBS volumes used for hot and cold data storage within the indexers. 

See below the steps followed for implementing the EBS-backed AMI data lifecycle policy:

1. Create a new tag for all the AWS Splunk servers except Indexers where
tag name = LifecyclePolicy and tag value = EBS-Backed-AMI
2. On the EC2 service page, select "Lifecycle Manager" and "Create Lifecycle Policy"
3. For the policy type, select "EBS-backed AMI policy"
4. Within the "Target resource tags" enter the values for the tag created in step 1
5. On the next page, select the following schedule:
Frequency
Every 24 hours starting at 04:00 UTC.
Retain rule
A maximum of 7 will be retained. The oldest AMI retained will be <= 7 days old.
6. Within the "Advanced Settings", select "Copy tags from source"
7. Review policy and save once everything looks good.

### **EBS snapshot policy**
This type of policy automates the creation, retention, and deletion of EBS snapshots, which means that this policy created snapshots of EBS volumes. We are currently using this policy for taking a back-up of the Root and the Temp EBS volumes attached to all the Splunk Indexers. 

See below the steps followed for implementing the EBS Snapshot Policy:

1. Create a new tag for all the Root and Tmp EBS volumes for the AWS Splunk Indexer servers where tag name = LifecyclePolicy and tag value = EBS-Policy
2. On the EC2 service page, select "Lifecycle Manager" and "Create Lifecycle Policy"
3. For the policy type, select "EBS snapshot policy"
4. Within the "Target resource tags" enter the values for the tag created in step 1. Also, select the "Target resource types" as "Volume"
5. On the next page, select the following schedule:
Frequency
Every 24 hours starting at 04:00 UTC.
Retain rule
A maximum of 7 will be retained. The oldest snapshot retained will be <= 7 days old.
6. Within the "Advanced Settings", select "Copy tags from source"
7. Review policy and save once everything looks good.
