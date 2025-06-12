#Playbook: How to create GEMS Health Monitoring Playbooks


This playbook is intended to help with the creation of playbooks that are required for GEMS Health Monitoring alerts. The below table shows which types of playbooks, work item types, work item types alerts, and area path. All GEMS Health Monitoring alerts can be found on [Global FC Splunk Monitoring](https://dev.azure.com/GlobalSOC/Splunk/_boards/board/t/Global%20FC%20Splunk%20Monitoring/Project). 



|**Playbook Type**| **Work Item Type**  | **Work Item Type from Alert**  | **Area Path** |

| Playbook: DMC -  | Health Monitoring Search | Health Monitoring Alert | Splunk\Global FC Engineering
| Playbook: SPM -| Performance Monitoring Search | Performance Monitoring Alert | Splunk\Global FC Run Content Team
| Playbook: DMC -  Indexes | Data Monitoring Search | Data Monitoring Alert | Splunk\Global FC Engineering | 
| Playbook: SecMon - | Splunk Security Monitoring Search | Security Monitoring Alert | Splunk\Global FC Engineering Leads | 

When formalizing a playbook for its appropriate alert the below templates are used as they associate to the Playbook type, Work Item Type, Work Item Type from Alert, Area path, and states on the Area path software development pipelines. 


##Playbook: DMC - <Alert>

An alert from the Distributed Monitoring Console (DMC) is triggered **<Alert Title>**. **<description of the alert>**
**Health Monitoring Alert Work Item (HMAWI)** is automatically created by Azure Logic and added to Global **FC Engineering board** on the "New" column. Also, an email is sent to DeloitteGlobalFusionEngineering@deloitte.com.

HMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution.

Run leads assign HMAWI work item to an available Run Engineer.

Run lead is responsible for managing Run Engineer workload to make sure resolution can be met within SLA.
Run Engineer starts resolution process by following alert-specific playbook.

**Insert steps of troubleshooting based off states on the board area path. Example below:** [Global FC Engineering](https://dev.azure.com/GlobalSOC/Splunk/_boards/board/t/Global%20FC%20Engineering/Project)

![Global FC Engineering.png](/.attachments/Global%20FC%20Engineering-18a58239-aa85-49f1-96d9-116ac4bdef85.png)


##Playbook: SPM - <Alert>

An alert from the Distributed Monitoring Console (DMC) **<Alert Title>. <description of the alert>**
**Search Performance Monitoring Alert Work Item (SPMAWI)** is automatically created by Azure Logic and added to **Global FC Run Content Team board** on the "New" column. Also, an email is sent to DeloitteGlobalFusionEngineering@deloitte.com

SPMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution.

Run leads assign SPMAWI work item to available Run Engineer.

Run lead is responsible for managing Run Engineer workload to make sure resolution can be met within SLA.
Run Engineer starts resolution process by following alert-specific playbook.

**Insert steps of troubleshooting based off alert and states on the board area path. Example below:** [Global FC Run Content](https://dev.azure.com/GlobalSOC/Splunk/_boards/board/t/Global%20FC%20Run%20Content%20Team/Tactical%20Content%20Task)

![Global FC Run Content Team.png](/.attachments/Global%20FC%20Run%20Content%20Team-17f4a2a4-cd4e-482a-acc4-cb938c268af6.png)

##Playbook: DMC – Indexes

An alert from the Distributed Monitoring Console (DMC) is triggered due to an index that is not receiving data for the specified threshold duration.

**Data Monitoring Alert Work Item (DMAWI)** is automatically created by Azure Logic and added to **Global FC Engineering board** on the "New" column. Also, an email is sent to DeloitteGlobalFusionEngineering@deloitte.com

DMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution.

Run leads assign DMAWI work item to available Run Engineer.

Run lead is responsible for managing Run Engineer workload to make sure resolution can be met within SLA.

Run Engineer starts resolution process by following alert-specific playbook.

**Insert steps of troubleshooting based off states on the board area path. Example below:** [Global FC Engineering](https://dev.azure.com/GlobalSOC/Splunk/_boards/board/t/Global%20FC%20Engineering/Project)

![Global FC Engineering.png](/.attachments/Global%20FC%20Engineering-cff352b2-30b5-4ee3-a253-9c3dfdbcf634.png)

##Playbook: SecMon - <Alert>

An alert from the Distributed Monitoring Console (DMC) is triggered

**Security Monitoring Alert Work Item (SMAWI)** is automatically created by Azure Logic App and added to **Global FC Engineering Leads team board**.

SMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution.

Email notification to Engineering leadership is sent with SMAWI description and link to SMAWI.

Global FC Engineering leadership assigns SMAWI work item to themselves.

Lead starts resolution process by following alert-specific playbook.

**Insert steps of troubleshooting based off states on the board area path. Example below:** [Global FC Engineering Leads](https://dev.azure.com/GlobalSOC/Splunk/_boards/board/t/Global%20FC%20Engineering%20Leads/Project)

![FC Engineering Leads.png](/.attachments/FC%20Engineering%20Leads-1db1a608-9000-4e17-a095-230ce8b7005d.png)


