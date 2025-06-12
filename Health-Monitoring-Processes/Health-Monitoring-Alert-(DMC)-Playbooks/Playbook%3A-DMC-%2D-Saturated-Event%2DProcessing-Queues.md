# **Playbook: DMC Alert - Saturated Event-Processing Queues**

An alert from the Distributed Monitoring Console (DMC) is triggered when One or more of your indexer queues is reporting a fill percentage, averaged over the last 15 minutes, of 90% or more.

Health Monitoring Alert Work Item (HMAWI) is automatically created by Azure Logic and added to Health Monitoring board on the &quot;New&quot; column. Also, an email is sent to [**deloittesiemhealthmonitoringteam@deloitte.com**](mailto:deloittesiemhealthmonitoringteam@deloitte.com) 

- HMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution.

- HM team assign HMAWI work item to an available HM member.

- HM team is responsible for managing HM team member workload to make sure resolution can be met within SLA.
 
- HM team member starts resolution process by following alert-specific playbook.

**Playbook: DMC Alert - Saturated Event-Processing Queues**

1. This alert will trigger if any Event processing queue&#39;s average queue fill percentage (last 15min) has filled up more than 90%. Event Processing Queues filling up leading to indexer stops completely.
2. HM team member moves the HMAWI to the &quot;Active&quot; column on the HM board.
3. HM team member accesses the Splunk GUI and verifies the veracity of the triggered alert by running the following query on the regional DMC Splunk server (usatramekj147) that is responsible for sending the alert.

```
| rest splunk_server_group=dmc_group_indexer /services/server/introspection/queues
| search title=tcpin_queue OR title=parsingQueue OR title=aggQueue OR title=typingQueue OR title=indexQueue
| eval fifteen_min_fill_perc = round(value_cntr3_size_bytes_lookback / max_size_bytes * 100,2)
| fields title fifteen_min_fill_perc splunk_server
| where fifteen_min_fill_perc > 90
| rename splunk_server as Instance, title AS "Queue name", fifteen_min_fill_perc AS "Average queue fill percentage (last 15min)"
```
1. HM team member annotates HMAWI with findings from the above query, as well as the time the query was executed.

2. From the Splunk results, you can see which Queue (indexQueue, typingQueue, aggQueue, parsingQueue) has been filled more than 90% on an average on which host.

![1.png](/.attachments/1-6ac889eb-c290-43e6-aa1c-192974bbee80.png)

3. Confirm the Queue, host(indexer) &amp; percentage from the alert. If not, the percentage may have gone to normal. Change the state of the HMAWI to **False Positive**.
4. If you still see the percentage as 90 for any of the queue for any indexer, please proceed and inform the Health Monitoring about the Issue.
5. After Trouble shooting the issue, verify the alert if the percentage for the queue in question has come down to normal.
6. After troubleshooting has been completed the HM team member will make sure to fully document all steps taken to resolve the issue as well as documenting the root cause and solution in the HMAWI.
7. HM team member will move the HMAWI to &quot;Closed&quot; and provide the stakeholder with the evidence obtained on previous step through email. The following DLs should be cc&#39;d [**deloittesiemhealthmonitoringteam@deloitte.com**](mailto:deloittesiemhealthmonitoringteam@deloitte.com)


1. Additional Troubleshooting steps if Issue still exists:

In case, while performing the above troubleshooting steps if HM team member faces any restriction like permission related issue reach out to the SIEM Engineering team for additional troubleshooting support.

If Architecture teams is unable to find root cause, then open Splunk Support case for further troubleshooting. When the solution is identified, HM team member updates the HMAWI to appropriate states (root cause identified, solution identified, solution implemented fields) on HMAWIs.

1. Then HM team member moves HMAWI to closed column &amp; state and notifies Health Monitoring team that issue has been resolved.

