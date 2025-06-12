# **Playbook: DMC Alert - Indexer Not Reachable**

An alert from the Distributed Monitoring Console (DMC) is triggered when an indexer is not reachable to its cluster master or any other indexers.

Health Monitoring Alert Work Item (HMAWI) is automatically created by Azure Logic and added to Health Monitoring board on the &quot;New&quot; column. Also, an email is sent to [**deloittesiemhealthmonitoringteam@deloitte.com**](mailto:deloittesiemhealthmonitoringteam@deloitte.com) 

HMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution

 HM team assign HMAWI work item to an available HM team member

 HM team is responsible for managing HM team member workload to make sure resolution can be met within SLA

HM team member starts resolution process by following alert-specific playbook

**Playbook: DMC Alert - Indexer Not Reachable**

1. HM team member moves the HMAWI to the &quot;Active&quot; column on the HM board
2. HM team member accesses the Splunk GUI and verifies the veracity of the triggered alert by running the following query on the regional DMC Splunk server that is responsible for sending the alert.

```
| inputlookup siem_architecture
| search ROLE="CyberSec Splunk Indexer"
| rename "NEW Host/VM" as host
| eval host = lower(host)
| table host ROLE
| join type=left host
    [| tstats latest(_time) as latest_Time where index=_internal by host
     | table host, latest_Time ]
| fillnull value="N" latest_Time
| eval threshold=now()-30
| table host latest_Time ROLE threshold
| where latest_Time < threshold
| convert ctime(latest_Time) ctime(threshold)
```
HM team member annotates HMAWI with findings from the above query, as well as the time the query was executed.

1. From the Splunk GUI navigate to Settings -> Indexer Clustering. If a host is showing a status of &#39;Down&#39; notify Health Monitoring by sending an email to [**deloittesiemhealthmonitoringteam@deloitte.com**](mailto:deloittesiemhealthmonitoringteam@deloitte.com) and proceed with the investigation.

![](RackMultipart20200717-4-gnui5q_html_10887e9cce5fc907.png)

2. Verify backend access to Indexer by using SSH to log into the server.
3. Ensure the &quot;Splunk Server&quot; is running by checking the status of Splunk.
 Sudo to the Splunk service account and execute the command below:
```./splunk status ```

Verify splunkd is running. If not, start Splunk with:

```./splunk start```

1. Check if the ICM status is good by logging into the backend of the ICM of appropriate environment and running the below query (Provide admin password if asked)

 &quot; **splunk show cluster-status –verbose&quot;**

 ![](RackMultipart20200717-4-gnui5q_html_8c53cc93f9228dea.png)
2. After troubleshooting has been completed the HM team member will make sure to fully document all steps taken to resolve the issue as well as documenting the root cause and solution in the HMAWI.
3. Then HM team member will move the HMAWI to &quot;Closed&quot; and provide the stakeholder with the evidence obtained on previous step through email. The following DLs should be cc&#39;d [**deloittesiemhealthmonitoringteam@deloitte.com**](mailto:deloittesiemhealthmonitoringteam@deloitte.com)


1. Additional Troubleshooting steps if Issue still exists:

If, while performing the above troubleshooting steps, HM team member faces any issues that are permission related reach out to the Engineering team for additional troubleshooting support.

If Architecture team is unable to find root cause, then open a Splunk Support case for further troubleshooting. When the solution is identified, Engineer updates the HMAWI to appropriate states (root cause identified, solution identified, solution implemented fields) on HMAWIs.

1. HM Team member moves HMAWI to closed column &amp; state and notifies Health Monitoring Team that issue has been resolved.