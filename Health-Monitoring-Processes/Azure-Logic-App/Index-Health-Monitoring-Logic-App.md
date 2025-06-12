###What: documentation of the automation solution that creates work items from Splunk email alerts 

###Term Definitions:
- Trigger: an event that must occur to trigger the various automated actions supported by Azure Logic
- Action: actions taken by Azure Logic after the trigger has been observed
- Condition: conditions that must be met for Azure Logic to execute subsequent automated actions 
- Compose: action used by Azure Logic to pass the output of a former step to subsequent steps of automation
- Dynamic Content: content (or result sets) created from an arbitrary step in Azure Logic that can be called in later steps of logic app
- Parameter: static parameters encoded into the logic app. Examples include SLA response time, Playbook, SLA priority etc

###Trigger: when a new email arrives in the "Health Alerts" folder of Shared Mailbox (dttlcapprojectssplun@deloitte.com) 
![health_monitoring_1.JPG](/.attachments/health_monitoring_1-8cbb84f1-5eab-4a85-900a-76a333bce4cd.JPG)
###Condition: check the email subject to see if it contains the string "index=" and does not contain "ACTION REQUIRED"
![condition.JPG](/.attachments/condition-7bca5673-6c39-4947-bf04-e122f5f93a89.JPG)
###Execute Javascript Code: used to extract the problem index from the email subject string
###Compose: used to pass the output of the javascript execution to subsequent automation steps
![javascript.JPG](/.attachments/javascript-9168da59-7264-4a54-b5e8-46d8bd37396a.JPG)
###Create a work item: action taken by Azure Logic to create a work item when former conditions in logic app succeed
- Organization Name always equals "GlobalSOC"
- Project Name always equals "Splunk"
- Work Item Type always equals "Health Monitoring Alert"
- Title is dynamic content taken from the email subject observed in the trigger
- Description is dynamic content taken from the email body observed in the trigger
- Area path always equals "Splunk\Global FC Engineering"
- Playbook: encoded as an azure logic parameter. Matches up to the alert name being triggered
- Problem Index: the index that is missing data
- SLA Priority: encoded as an Azure Logic parameter. Defined by Project S leadership
- SLA Response Time in Hours: is "SLA Priority" translated to hours
- Time of alert: the time the alert was triggered
- dummy field name: denotes when the work item will have elapsed SLA. Appears in devops as "Out of SLA On"
- hidden out of SLA on: hidden field on work item that corresponds to when the work item will have elapsed SLA. Used for timestamp math in future steps
- Assigned to: always equals Mamatha Pannala for health monitoring alert work items
![create_work_item.JPG](/.attachments/create_work_item-4044e825-ddbe-479c-b061-e729ea38895f.JPG)
###Update a work item: used to lock (make read only) SLA details of work items created
- Organization name always equals GlobalSOC
- Work item Id: dynamic content passed in from the create a work item step
- zebra field: always equals "not needed". This field is required to make SLA details read only
![update_work_item.JPG](/.attachments/update_work_item-dfbd441c-c8b7-47b7-83fa-c101589d098c.JPG)
###Send an email (v2): used to send a follow up email to team leads that work item has been created
- Body: should always say "Splunk Health Monitoring Alert has been triggered, please investigate and assign to a team member by naigating to the following URL: 'https://dev.azure.com/GlobalSOC/Splunk/_workitems/edit/<dynamic content work item ID>"
- Subject: should always say "[ACTION REQUIRED]<dynamic content work item title>"
- To: enter team lead email addresses separated by ";"
- Importance: should always equal "High"
![send_an_email.JPG](/.attachments/send_an_email-5b137c3c-e448-46d5-a233-d4525c4e2364.JPG)