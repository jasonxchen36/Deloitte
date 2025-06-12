###What: documentation of the automation solution that creates work items from Splunk email alerts 

###Term Definitions:
- Trigger: an event that must occur to trigger the various automated actions supported by Azure Logic
- Action: actions taken by Azure Logic after the trigger has been observed
- Condition: conditions that must be met for Azure Logic to execute subsequent automated actions
- Compose: action used by Azure Logic to pass the output of a former step to subsequent steps of automation
- Dynamic Content: content (or result sets) created from an arbitrary step in Azure Logic that can be called in later steps of logic app
- Parameter: static parameters encoded into the logic app. Examples include SLA response time, Playbook, SLA priority etc
 ###Trigger: when a new email arrives in the <Mailbox Sub-folder receiving the relevant alert> folder
![Screen Shot 2020-11-08 at 4.39.39 PM.png](/.attachments/Screen%20Shot%202020-11-08%20at%204.39.39%20PM-36d07118-6865-4f2d-b73f-0b3ceeb7f466.png)

###Azure Function Trigger: Launch the relevant Azure Function to classify the alert by checking for the identifier string in the email subject
![Screen Shot 2020-11-08 at 5.08.47 PM.png](/.attachments/Screen%20Shot%202020-11-08%20at%205.08.47%20PM-61f133d6-8298-47cb-bb6e-d2c1ada8fff5.png)

###Switch: Based on the classification by the Azure Functions, switch determines the workflow to trigger
![Screen Shot 2020-11-08 at 5.23.09 PM.png](/.attachments/Screen%20Shot%202020-11-08%20at%205.23.09%20PM-7521c0ee-c465-4341-9bfb-2062d6ef0578.png)

###Execute Javascript Code: used to perform text extractions from the email (e.g. Extracting the problem index from the email subject string)
![Screen Shot 2020-11-08 at 5.23.53 PM.png](/.attachments/Screen%20Shot%202020-11-08%20at%205.23.53%20PM-95f4b618-dd5d-490f-bc78-7e362cb0fcc6.png)

###Compose: used to pass the output of the javascript execution to subsequent automation steps
![Screen Shot 2020-11-08 at 5.24.35 PM.png](/.attachments/Screen%20Shot%202020-11-08%20at%205.24.35%20PM-fa50a83f-9709-4717-aee2-ec3506de5681.png)

###Create a work item: action taken by Azure Logic to create a work item when former conditions in logic app succeed
- Organization Name always equals "GlobalSOC"
- Project Name always equals "Splunk"
- Work Item Type depends on the alert WI to be created in DevOps for the relevant alert
- Title is dynamic content taken from the email subject observed in the trigger
- Description is dynamic content taken from the email body observed in the trigger
- Area path is the team to which to send the alert WI and depends on the relevant alert
- Playbook: encoded as an azure logic parameter. Matches up to the alert name being triggered
- SLA Priority: encoded as an Azure Logic parameter. Defined by Project S leadership
- SLA Response Time in Hours: is "SLA Priority" translated to hours
- Time of alert: the time the alert was triggered
- SLA Expires: denotes when the work item will have elapsed SLA.
- hidden out of SLA on: hidden field on work item that corresponds to when the work item will have elapsed SLA. Used for timestamp math in future steps
![Screen Shot 2020-11-08 at 5.25.45 PM.png](/.attachments/Screen%20Shot%202020-11-08%20at%205.25.45%20PM-57b406a6-e58d-419c-b99a-4fdbe3dc5c22.png)

###Update a work item: used to lock (make read only) SLA details of work items created
- Organization name always equals GlobalSOC
- Work item Id: dynamic content passed in from the create a work item step
- SLA Read Only: This is set to "true". This field is required to make SLA details read only
![Screen Shot 2020-11-08 at 5.28.18 PM.png](/.attachments/Screen%20Shot%202020-11-08%20at%205.28.18%20PM-21620d80-8bf8-41f2-9680-55cf93eed0ec.png)

###Send an email (v2): used to send a follow up email to team leads that work item has been created
- Body: should always say "Splunk Health Monitoring Alert has been triggered, please investigate and assign to a team member by naigating to the following URL: 'https://dev.azure.com/GlobalSOC/Splunk/_workitems/edit/<dynamic content work item ID>"
- Subject: should always say "[ACTION REQUIRED]<dynamic content work item title>"
- To: enter team lead email addresses separated by ";"
- Importance: Assigned based on importance determined for the relevant alert by team and leadership
![Screen Shot 2020-11-08 at 5.29.36 PM.png](/.attachments/Screen%20Shot%202020-11-08%20at%205.29.36%20PM-641f316f-8278-4843-90dc-13d8c5ddccf5.png)