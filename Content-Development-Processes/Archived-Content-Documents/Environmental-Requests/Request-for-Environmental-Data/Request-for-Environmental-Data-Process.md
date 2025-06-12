**What is a Request for Environmental Data?**
Request for Environmental Data: This Work Item should be used when you are requesting any sort of environmental data, for example-IP addresses of servers, Approved File Sharing Apps, List of accounts that need to be whitelisted/Monitored--that will help us create high fidelity alerts. Referential Environmental data is crucial to help us build and maintain high fidelity alerts and eliminate false positives for the Monitoring Team.

# **Process for Requesting Environmental Data** 

Scenario: An Alert in Volume Testing/Production produces a false positive (determined after investigation)

1.Engineer or Analyst Creates a Request for Environmental Data Work Item, following these guidelines seen [here](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/532/RFED-Work-Item). 

  - **Required fields:**
    - Assigned to: Describes who will be taking point on this work item.
    - State
    - Area: Splunk \ Global Environmental Issues Team    
    - Description
    - Region
    - Data Requested
    - Related Work: Link the corresponding Build Content Task/s
    - Stakeholder

2. Once the Work Item is created, Reach out to the appropriate Stakeholder using the [Request for Referential Data Email Template.](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/459/RFED-Email-Template) 

3. After the Assignee has reached out to the stakeholder, change the state of the item from _New to ATTN Stakeholder_

4. Upon the stakeholder responding, please change the state from ATTN Stakeholder to ATTN Project S-- if further research or work needs to be done from our side.
    
    _Note: If after 7 days there has been no change in WI State, the assignee will receive a friendly reminder to follow up with the stakeholder or complete the necessary work on their end._
   
    _Note: If after 14 days there has been no change in WI State and it remains in ATTN Stakeholder, the Work item will be escalated. The GEMS Owner and GEMS Regional Service Leads will receive a notification to escalate the request with the Stakeholder. Escalations will be tracked in this [dashboard](https://dev.azure.com/GlobalSOC/Splunk/_dashboards/dashboard/bbc0845d-812c-42de-aa8a-61b290872472), and via Splunk Alerts. (coming soon:Azure Functions)_ 
   
    _Note: The Assignee is also responsible for creating a ServiceNow Ticket for Escalation if the Stakeholder has been unresponsive for 14 days. Please follow these [steps](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/526/ServiceNow-Ticket-Escalation-Process)._


5. After the data is received, please set the Data Received Boolean as "true", and if the Data needs to be refreshed/updated change the Refresh Required Boolean to True and fill out the Refresh Date Time Picker field. 

    _Upcoming Refresh Dates will be monitored [here](https://dev.azure.com/GlobalSOC/Splunk/_dashboards/dashboard/bbc0845d-812c-42de-aa8a-61b290872472), and in the future the Assignee will receive a notification via Azure Functions to reach out to the Stakeholder regarding this updated data_
 
    _*Once you receive refreshed data, update the refresh date for the next refresh or turn the boolean to false if there is no more data that is going to be updated_  

6. If the data received happens to be a spreadsheet or able to be converted into a spreadsheet, create a lookup and upload to Splunk to the DA-ESS-<region>-Lookups App. Once you upload the lookup to Splunk, create a Lookup Work Item and link it to the Request for Environmental Data, and add the filter name to the Work Item as seen in the [WI Process](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/532/RFED-Work-Item)
    _Note: Data that needs to be refreshed, please mark so in the Lookup Item and include the Refresh Date if it can not be retrieved programatically_

7. Once all of this is done, Close out the Work Item. 
   _Note: If a SNOW Ticket was raised, the ticket must be completed and logged in the "Escalationn Description" before the Work Item can be closed out._
