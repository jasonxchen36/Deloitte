**What is a Request for Environmental Data?**
Environmental Fix: Environmental Fix Items are used to raise source device/ IT ecosystem errors or misconfigurations to the wider attention of the Deloitte IT audience.

# **Process for Environmental Fix** 

Scenario: An Alert in Volume Testing/Production produces a false positive (determined after investigation) due to an issue within our environment (i.e bad configuration)

1.Engineer or Analyst Creates an Environmental Fix Work Item, following these guidelines seen [here](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/528/EF-Work-Item). 

  - **Required fields:**
    - Assigned to: Describes who will be taking point on this work item.
    - State
    - Area: Splunk \ Global Environmental Issues Team    
    - Description
    - Region
    - Fix Requested
    - Related Work: Link the corresponding Build Content Task/s
    - Stakeholder

2. Once the Work Item is created, Reach out to the appropriate Stakeholder using the [Environmental Fix Email Template.](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/541/EF-Email-Template) 

3. After the Assignee has reached out to the stakeholder, change the state of the item from _New to ATTN Stakeholder_

4. Upon the stakeholder responding, please change the state from ATTN Stakeholder to ATTN Project S-- if further research or work needs to be done from our side.
    
    _Note: If after 7 days there has been no change in WI State, the assignee will receive a friendly reminder to follow up with the stakeholder or complete the necessary work on their end._
   
    _Note: If after 14 days there has been no change in WI State and it remains in ATTN Stakeholder, the Work item will be escalated. The GEMS owners will receive a notification to escalate the request with the Stakeholder. Escalations will be tracked in this [dashboard](https://dev.azure.com/GlobalSOC/Splunk/_dashboards/dashboard/bbc0845d-812c-42de-aa8a-61b290872472), and via Splunk Alerts. (coming soon:Azure Functions)_ 
   
    _Note: The Assignee is also responsible for creating a ServiceNow Ticket for Escalation if the Stakeholder has been unresponsive for 14 days. Please follow these [steps](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/526/ServiceNow-Ticket-Escalation-Process)._


5. Once the Fix has been resolved, Verify the changes on Staging (if applicable) and then Production. If the changes are correct, change the Fix Implemented Boolean to True and attach any necessary attachments (approvals, knowledge, etc.)

7. Once all of this is done, Close out the Work Item. 