There are two types of false positives:

- The person did what was reported, but had a good reason to do so
  - Move the work item to the resolve state 
  - Since Splunk will automatically update, manually go into Splunk and delete the aforementioned offense for said offender
- The alert didn&#39;t work properly (logic wasn&#39;t working appropriately)
  - Alert requires additional tuning; engineer verifies findings with Global FC Engineering leads
  - Engineer updates BIWI or SMAWI state to False Positive
  - Since Splunk will automatically update, manually go into Splunk and delete the aforementioned offense for said offender
  - Engineer creates Tactical Content Work Item (TCWI) and links to BIWI or SMAWI and also links to the Splunk Security Monitoring Search Work Item (main work item associated with Alert)
  - Engineer works with other Global FC Engineers to tune the alert
  - Once tuned, Engineer updates TCWI state to Ready for Test and makes updates to the Splunk Security Monitoring Search Work Item
  - Engineer then updates alert logic and/or filters in DMC
  - Engineer verifies logic is firing appropriately
  - Once verified, Engineer updates TCWI state to Verified/Closed 