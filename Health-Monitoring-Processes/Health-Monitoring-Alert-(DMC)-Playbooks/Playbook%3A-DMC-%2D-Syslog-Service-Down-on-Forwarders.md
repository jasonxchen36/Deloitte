# **Playbook: DMC - Syslog Service Down on Forwarders**

An alert from the Splunk SHC is triggered when the Syslog service is not running on a monitored forwarder.

Health Monitoring Alert Work Item (HMAWI) is automatically created by Azure Logic and added to Health Monitoring board on the &quot;New&quot; column. Also, an email is sent to [**deloittesiemhealthmonitoringteam@deloitte.com**](mailto:deloittesiemhealthmonitoringteam@deloitte.com)

HMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution

HM team assign HMAWI work item to available HM team member.


HM team is responsible for managing HM team member workload to make sure resolution can be met within SLA.

HM team member starts resolution process by following alert-specific playbook

**Playbook: DMC - Syslog Service Down on Forwarders**

1. HM team member moves HMAWI to &quot;Active&quot; column on HM board
2. HM team member accesses the Splunk GUI and verifies the veracity of the triggered alert by running the following query on the regional DMC Splunk server that is responsible for sending the alert

```
index=*_splunkcore_endpoint_nix sourcetype=ps process_name=rsyslogd
  [| inputlookup siem_architecture
   | search ROLE="CyberSec Syslog*"
   | rename "NEW Host/VM name" as host
   | table host]
| stats latest(_time) as lastSeen by host
| eval diff=relative_time(now(), "-5m@m")-lastSeen
| eval status=if(diff>3600,"stopped","running")
| search status="stopped"
| eval lastSeen=strftime(lastSeen, "%c")
| table host lastSeen status
```

HM team member annotates HMAWI with findings from the above query, as well as the time the query was executed.

1. Verify backend access to Indexer by using SSH to log into the server.
2. Ensure the syslog service is running by performing the following command
_ **sudo service rsyslog status** _

![](RackMultipart20200717-4-wtkrzm_html_63e06cf269e9c0a3.png)

3. You should be able to see &quot;Active (running)&quot; in the output of the above command. If not, Start the rsyslog service by running the below command.

_ **sudo service rsyslog start** _

Additionally, ensure the &quot;Splunk Server&quot; is running by checking the status of Splunk.
 Sudo to the Splunk service account and execute the command below:
```./splunk status```

Verify splunkd is running. If not, start Splunk with:

```./splunk start```

1. After troubleshooting has been completed the HM team member will make sure to fully document all steps taken to resolve the issue as well as documenting the root cause and solution in the HMAWI.
2. Then HM team member will move the HMAWI to &quot;Closed&quot; and provide the stakeholder with the evidence obtained on previous step through email. The following DLs should be cc&#39;d [**deloittesiemhealthmonitoringteam@deloitte.com**](mailto:deloittesiemhealthmonitoringteam@deloitte.com)


1. Additional Troubleshooting steps If Issue still exists:

If, while performing the above troubleshooting steps, the HM team member faces any issues that are permission related reach out to the Engineering team for additional troubleshooting support.

If Engineering teams is unable to find root cause, then open a Splunk Support case for further troubleshooting. When the solution is identified, Engineer updates the HMAWI to appropriate states (root cause identified, solution identified, solution implemented fields) on HMAWIs.

1. HM team member moves HMAWI to closed column &amp; state and notifies HM team that issue has been resolved.