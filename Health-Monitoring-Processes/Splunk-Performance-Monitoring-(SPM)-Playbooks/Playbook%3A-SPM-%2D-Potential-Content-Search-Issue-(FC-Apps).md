**[Alert is under Review]()**

# **Playbook: SPM - Potential Content Search Issue (FC Apps)** 

- An alert from the Distributed Monitoring Console (DMC) is triggered due to an acceleration running in a non-approved app. This should be disabled at earliest convenience.
- Search Performance Monitoring Alert Work Item (SPMAWI) is automatically created by Azure Logic and added to Health Monitoring Team board on the "New" column. 
- SPMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
- Health Monitoring Team will assign SPMAWI work item to available Team member.
- Health Monitoring Team is responsible for managing workload among the resources to make sure resolution can be met within SLA
- Health Monitoring Team starts resolution process by following alert-specific playbook

**Playbook:** **SPM - Potential Content Search Issue (FC Apps)**

SPM - Potential Content Search Issue (FC Apps):

1.  Health Monitoring Team member moves SPMAWI to "Active" column on Global FC Run Content Team board
2. Health Monitoring Team member accesses Splunk GUI and verifies the veracity of the triggered alert by running the following query and checking if results are the same as the received on the SPMAWI:

index=\_internal sourcetype=scheduler (app=&quot;DA-ESS-FC\*&quot; OR app=&quot;\*MF\_Content&quot;)
| stats count(eval(status==&quot;success&quot;)) AS successCount count(eval(status==&quot;continued&quot; OR status==&quot;skipped&quot; OR status==&quot;delegated\_remote\_error&quot;)) as failedCount count as orig\_count avg(run\_time) as avg\_run\_time median(run\_time) as median\_run\_time max(run\_time) as max\_run\_time min(run\_time) as min\_run\_time by savedsearch\_name, app, host| where orig\_count\=288 OR failedCount\=successCount| fields savedsearch\_name host app orig\_count successCount failedCount avg\_run\_time median\_run\_time max\_run\_time min\_run\_time| sort - orig\_count


When finished with above steps, Health Monitoring Team member will follow the steps provided below:


1. This original intent behind this alert is Alerts if a saved search is running more frequently than the lowest configured cron (288 searches/24 hours). That is for every 5 min. This alert will trigger when it caught any alert running for less than a 5 min frequency.
2. This alert also triggers if the number of failed saved search attempts is greater than the number of successful saved search attempts.
3. If you see a single host is the reason for multiple searches getting failed, Troubleshoot in the viewpoint of searchhead(host).The problem might reside in the search head itself.(Login to that search head, click the &quot; **I**&quot; icon beside the username and see if anything is appearing in the red state). If so, Contact the infra team regarding the issue.

 ![image.png](/.attachments/image-e2eb0363-45c9-431c-9dcc-3dcd28e8f161.png)


4. If you see search head isn&#39;t the issue which means you should be seeing multiple hosts for multiple saved searches. If that&#39;s the case, Check the cron schedule for the saved search name.
5. You can do it in GUI or backend. It is not safe to view configurations in GUI, we can mess with the settings easily. However, it will be safe to check this in DevOps.

DevOps -> SHC -> SHC_AMER -> <<App Name>>  -> default -> savedsearches.conf -> <<Alert Name>> -> #Alert Settings -> “Look for cron _schedule”

 ![image.png](/.attachments/image-8aff5e2c-fa58-4e80-b85b-20297d6ac53c.png)

6. If you don&#39;t understand the cron\_schedule, take the help of website like crontab.guru. copy the crontab can paste it the website.

 For example, in the below screenshot the query is scheduled to run on every 5 min. (12 times \* 24 hours = 288 times per day )

 ![image.png](/.attachments/image-c4a621b6-34ff-4c29-b39c-1aa76f23be87.png)![](RackMultipart20200630-4-vtad43_html_c9e14eba412b616b.png)

7. If you see the problem neither resides in the search head nor in the cron schedule, then check the query itself.
8. Pick one of the saved searches from the results and run the search in one of the search heads and see if the search is running successfully. If you see any problem with the query taking too long to run or failing to finish itself then contact content teams about the query/alert.


9. Include this information as a comment on the SPMAWI. After completing Troubleshooting and resolving the problem, Then Health Monitoring Team member will move the SPMAWI to "Completed" and inform the stake holder/creator with the evidence obtained on previous step through email cc'ed  deloittesiemhealthmonitoringteam@deloitte.com**.

Additional Troubleshooting steps:

1. While performing the above troubleshooting steps if Health Monitoring team member faces any restriction like permission related issue for enabling disabling acceleration reach out to the SIEM Engineering team for additional troubleshooting support.
2. If SIEM Engineering teams is unable to find root cause, then open Splunk Support case for further troubleshooting
3. Health Monitoring team member updates root cause identified, solution identified, solution implemented fields on SPMAWIs
4. Health Monitoring team member moves SPMAWI to closed column & state
5. Health Monitoring team member notifies Health Monitoring team that issue has been resolved.