**Alert is disable in EMEA AND APAC**

# **Playbook: DMC Alert - Hot/Cold disk not re-mounted on the Indexer**

An alert from the Distributed Monitoring Console (DMC) is triggered when an indexer is not reachable to its cluster master or any other indexers.

Health Monitoring Alert Work Item (HMAWI) is automatically created by Azure Logic and added to Health Monitoring board on the &quot;New&quot; column. Also, an email is sent to [**deloittesiemhealthmonitoringteam@deloitte.com**](mailto:deloittesiemhealthmonitoringteam@deloitte.com) 

HMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution. 

HM team assign HMAWI work item to an available HM team member

HM team is responsible for managing HM team member workload to make sure resolution can be met within SLA

HM team member starts resolution process by following alert-specific playbook

**Playbook: DMC Alert - Hot/Cold disk not re-mounted on the Indexer**

1. This alert will trigger if any of the 3 mount points(splunkcoldlv, splunkhotlv, splunklv) is missing from the filesystem.
2. HM team member moves the HMAWI to the &quot;Active&quot; column on the Health Monitoring board.
3. HM team member accesses the Splunk GUI and verifies the veracity of the triggered alert by running the following query on the regional DMC Splunk server that is responsible for sending the alert.

```
index=*_splunkcore_endpoint_nix sourcetype=df Filesystem IN (/dev/mapper/splunkcoldvg-splunklv,/dev/mapper/splunkcoldvg-splunkcoldlv,/dev/mapper/splunkhotvg-splunkhotlv)
   [| inputlookup siem_architecture
    | search ROLE="CyberSec Splunk Indexer"
    | rename "NEW Host/VM" as host
    | table host]
| stats values(Filesystem) as activeMountFs values(mount) as activeMount dc(Filesystem) as activeCount by host
| search activeCount<3
| eval inactiveMount=if(match(activeMountFs,&quot;splunkhotlv&quot;) AND match(activeMountFs,&quot splunkcoldlv&quot;) AND match(activeMountFs,&quot;splunklv&quot;), &quot;&quot;,
    if(match(activeMountFs,&quot;splunkhotlv&quot;) AND match(activeMountFs,&quot;splunkcoldlv&quot;), &quot;/opt/splunk&quot;,
    if(match(activeMountFs,&quot;splunklv&quot;) AND match(activeMountFs,&quot;splunkcoldlv&quot;), &quot;/opt/splunk/var/lib/splunk/hot&quot;,
    if(match(activeMountFs,&quot;splunklv&quot;) AND match(activeMountFs,&quot;splunkhotlv&quot;), &quot;/opt/splunk/var/lib/splunk/cold&quot;,
    if(match(activeMountFs,&quot;splunkhotlv&quot;), &quot;/opt/splunk;/opt/splunk/var/lib/splunk/cold&quot;,
    if(match(activeMountFs,&quot;splunkcoldlv&quot;), &quot;/opt/splunk;/opt/splunk/var/lib/splunk/hot&quot;,
    if(match(activeMountFs,&quot;splunklv&quot;), &quot;/opt/splunk/var/lib/splunk/cold;/opt/splunk/var/lib/splunk/hot&quot;, &quot;/opt/splunk;/opt/splunk/var/lib/splunk/cold;/opt/splunk/var/lib/splunk/hot&quot;)))))))
| makemv delim=&quot;;&quot; inactiveMount
| table host inactiveMount
```
HM team member annotates HMAWI with findings from the above query, as well as the time the query was executed.

1. From the Splunk results, check the host &amp; mount point which is missing from it. Login to the backend of that host and run the command &quot;_ **df -h** _&quot;.
2. Check if the 3 mount points(splunkcoldlv, splunkhotlv, splunklv) are present in the filesystem. If yes, Close the alert as &quot;False Positive&quot;.

![DMC1.png](/.attachments/DMC1-1daf25b2-6bfc-4060-a61e-cccade4cb257.png)

1. Check if the filesystem which is missing from the query results, matches with actual filesystem which is missing in the backend.

Check which file system is missing and notify the HM Team ([deloittesiemhealthmonitoringteam@deloitte.com](mailto:deloittesiemhealthmonitoringteam@deloitte.com)) about the missing filesystem along with the host.

1. After troubleshooting has been completed the HM team member will make sure to fully document all steps taken to resolve the issue as well as documenting the root cause and solution in the HMAWI.
2. Then HM team member will move the HMAWI to &quot;Closed&quot; and provide the stakeholder with the evidence obtained on previous step through email. The following DLs should be cc&#39;d [**deloittesiemhealthmonitoringteam@deloitte.com**](mailto:deloittesiemhealthmonitoringteam@deloitte.com)


1. Additional Troubleshooting steps if Issue still exists:

In case, while performing the above troubleshooting steps if HM team member faces any restriction like permission related issue reach out to the Engineering team for additional troubleshooting support.

If Engineering teams is unable to find root cause, then open Splunk Support case for further troubleshooting. When the solution is identified, HM team member updates the HMAWI to appropriate states (root cause identified, solution identified, solution implemented fields) on HMAWIs.

1. Then the HM team member moves HMAWI to closed column &amp; state and notifies Health Monitoring team that issue has been resolved.