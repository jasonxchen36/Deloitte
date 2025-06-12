**Objective:** The purpose of this alert is to outline the steps to be followed when an alert is triggered due to data being found in an index while monitoring is turned off. The goal is to ensure appropriate actions are taken to address the alert promptly and efficiently.

Health Monitoring team member identifies an index which is feeding data while monitoring is disabled.  Please follow the below steps:
 
**Identification of the Alert:**
   - An alert will be triggered from Splunk SHC if data is detected in an index while monitoring is turned off.
   - This alert serves as a notification to take necessary action regarding the data found in the index.
   - Upon alert triggering, a work item will be created and assigned to the Health Monitoring team.
   - The WI will include relevant details such as the index name, last connected time, current time, difference in last connected and current time, Assignment Group, Region, Priority, Threshold. 
   - The HM team lead will assign the WI# to an available HM engineer for further investigation and resolution.
 
**Verification of the Alert:**
   - The assigned HM engineer will verify the alert by checking the raw data in the index in Splunk for the past 24 hours.
   - If the alert is determined to be a false positive, the HM engineer will update the WI# status to "False Positive."
   - A False Positive result should be evaluated in-depth along with the logic of the alert. If alert logic needs to be updated, a PR should be created and reviewed.  
   - If the alert is confirmed to be legitimate, the HM engineer will report this via email to the Data Management team(DT - Cyber Defense Engineering - Data Management dt-cyberdefenseengineering-datamanagement@deloitte.com), copying the HM team <DT - Cyber Defense Engineering - Health Monitoring deloittesiemhealthmonitoringteam@deloitte.com.
   - The email will seek clarification on whether the incoming data to the index is expected behavior or not. Additionally, seek further explanation on why monitoring status in the lookup does not match the data feed.
   - If the index is expected to receive the data, the HM engineer will send an email to the Splunk Architecture team(<DT - Cyber Defense Engineering - Architecture dt-cyberdefenseengineering-architecture@deloitte.com), requesting them to enable monitoring for the index.
   - The HM engineer will add a screenshot once from the lookup by running below command:
```AMER: |inputlookup Index_Mapping_AMER | search index=<index_name>```
```APAC:  |inputlookup Index_Mapping_APAC| search index=<index_name>```
```EMEA: |inputlookup Index_Mapping_EMEA | search index=<index_name>```
   - If the index is not supposed to have data, but data is still found in Splunk, the HM engineer will seek confirmation from the Data Management team.
   - Upon confirmation, the HM engineer will disable the inputs.conf file for the respective data source to prevent further data ingestion.
-The engineer will track the behavior of the index closely post any changes
 
**Index Removal (Optional):**
   - In cases where the index is deemed unnecessary and needs to be removed, the HM team will create a pull request to remove the index stanza from the respective indexer cluster configuration.
 
**WI Closure:**
   - Once the necessary steps have been performed and the alert has been appropriately addressed, the HM team will close the WI#, indicating the completion of the process.
 
**Note:** Throughout the entire process, clear communication and collaboration between the HM team, Data Management team, and Splunk Architecture team are crucial to ensure timely and accurate resolution of the alert.
