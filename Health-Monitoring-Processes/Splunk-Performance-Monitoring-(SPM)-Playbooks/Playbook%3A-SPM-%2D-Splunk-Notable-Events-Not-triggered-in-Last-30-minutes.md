# **Playbook: SPM - Splunk Notable Events Not triggered in last 30 minutes**

An alert from the Distributed Monitoring Console (DMC) is triggered due to Splunk Notable Events Not triggered in last 30 minutes.    

Search Performance Monitoring Alert Work Item (SPMAWI) is automatically created by Azure Logic and added to SIEM Engineering Team board on the &quot;New&quot; column. Also, an email is sent to [**DT - Cyber Defense Engineering - Health Monitoring **](mailto:deloittesiemhealthmonitoringteam@deloitte.com) and [**DT - Cyber Defense Engineering - Content Development **](mailto:dtcyberdefenseengineeringcontentdevelopment@deloitte.com)

SPMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution

Engineer assign SPMAWI work item to available Engineer

Engineer is responsible for managing Engineer workload to make sure resolution can be met within SLA

Engineer starts resolution process by following alert-specific playbook

**Playbook:**   **SPM - Splunk Notable Events Not triggered in last 30 minutes**

SPM - Splunk Notable Events Not triggered in last 30 minutes:

1. Engineer moves SPMAWI to &quot;Active&quot; column on Content Team board
2. Engineer accesses Splunk GUI and verifies the veracity of the triggered alert by running the following query and checking if results are the same as the received on the SPMAWI:

```
index=notable sourcetype=stash 
[ search index=_internal source=*scheduler.log*
NOT savedsearch_name="DEV\*" "sn_sec_multi_event_alert" | stats count by savedsearch_name
| rename savedsearch_name as search_name | table search_name ]
| stats values(node) as nodes,count as volume by _time,search_name
```

When finished with above steps, Engineer will follow the steps provided below:



1. Check if the &quot;notable&quot; index has data till now (index=notable). recent logs. Run the below query. If you find logs till the recent time, change the status to **False Positive.**
2. If not, Firstly check if the Splunk Environment is stable. Login to the Indexer Cluster Master of appropriate environment and navigate to Settings -\&gt; Indexer Clustering. Check if all the indexers &amp; Search heads are up. Check if Search factor is Met and All data is searchable.

![SPM 1.png](/.attachments/SPM%201-34fab832-1643-42e4-8875-5642fde2827f.png)

3. You should be seeing High Number of instances are down if environment is Unstable. In such critical cases, Mail to [**DT - Cyber Defense Engineering - Health Monitoring **](mailto:deloittesiemhealthmonitoringteam@deloitte.com) and [**DT - Cyber Defense Engineering - Content Development **](mailto:dtcyberdefenseengineeringcontentdevelopment@deloitte.com).
4. If you see a single host or two, it should be most possibly a known activity. Please proceed with further investigation.

1. Check if the Notable action is enabled for the alert in the question. Goto -\&gt; DevOps -\&gt; SHC -\&gt; SHC\_AMER -\&gt; \&lt;\&lt;App Name\&gt;\&gt; -\&gt; default -\&gt; savedsearches.conf -\&gt; \&lt;\&lt;Alert Name\&gt;\&gt; -\&gt; #Notable Event Settings -\&gt; \&lt;Confirm if the value for the action.notable = 1\&gt;
![SPM2.png](/.attachments/SPM2-e29ffb55-a0a3-4c64-92df-29afcb8f3cab.png)


1. If you see the value for the action.notable = **0** , which means the notable action has been disabled for this alert. Notify the content team about that.

1. Pick one of the saved searches from the results and run the search in one of the search heads and see if the search is running successfully. If you see any problem with the query taking too long to run or failing to finish itself then contact content teams about the query/alert.
2. Include this information as a comment on the SPMAWI. After completing Troubleshooting and resolving the problem, Then Engineer will move the SPMAWI to &quot;Closed&quot; and inform the stake holder/creator with the evidence obtained on previous step through email cc&#39;ed [**DT - Cyber Defense Engineering - Health Monitoring **](mailto:deloittesiemhealthmonitoringteam@deloitte.com) and [**DT - Cyber Defense Engineering - Content Development **](mailto:dtcyberdefenseengineeringcontentdevelopment@deloitte.com) 

*Additional Troubleshooting steps:*

1. While performing the above troubleshooting steps if Engineer faces any restriction like permission related issue for enabling disabling acceleration reach out to the Architecture team for additional troubleshooting support.

If SIEM Engineering teams is unable to find root cause, then open Splunk Support case for further troubleshooting

1. Engineer moves SPMAWI to closed column &amp; state
2. Engineer notifies Architecture team that issue has been resolved.