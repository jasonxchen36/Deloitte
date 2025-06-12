
**Playbook: DMC Alert – Potential KV Store Issue**

- An alert from the Distributed Monitoring Console (DMC) is triggered due to an issue with the KV store issue in the appropriate region.
- Health Monitoring Alert Work Item (HMAWI) is automatically created by Azure Logic and added to SIEM Engineering board on the &quot;New&quot; column. Also, an email is sent to [**DT - Cyber Defense Engineering - Health Monitoring **](mailto:deloittesiemhealthmonitoringteam@deloitte.com)
- HMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
- SIEM Engineer Lead will assign HMAWI work item to available Engineer
- SIEM Engineer Lead is responsible for managing Engineer workload to make sure resolution can be met within SLA 
- Engineer starts resolution process by following alert-specific playbook

**Playbook: DMC Alert – Potential KV Store Issue**
  
DMC Alert – Potential KV Store Issue

1. Engineer moves HMAWI to &quot;Active&quot; column on SIEM Engineering board
   1. Log into the shell of any KV store member.
   1. Navigate to the bin subdirectory in the Splunk Enterprise installation directory.
      `./splunk show kvstore-status` 
The command line returns a summary of the KV store member you are logged into, as well as information about every other member in the KV store cluster.

   1. Look at the replicationStatus field and identify any members that have neither &quot;KV store captain&quot; nor &quot;Non-captain KV store member&quot; as values will be considered as out of sync.


![image.png](/.attachments/image-f78df966-ded0-46f9-b0f8-b1a621e50754.png)


  4. Take the approval from SIEM team leads, for proceeding further on resyncing the KV store.


When finished with above steps, engineer will follow the steps provided below:

1. Identify how many Members are showing the KV store status out of sync. 
`./splunk show kvstore-status`

1. Make sure that Kv store captain is not same as SHC cluster captain, If it does then change the SHC cluster captain to another member.
2. Take back up of KV store on affected member
`./splunk backup kvstore`

By default, KV store backup would be taken on /opt/splunk/var/lib/splunk/kvstorebackup.

4. Stop splunk on affected member
`./splunk stop`

1. Then run./splunk clean kvstore --local. Command and answer &quot;y&quot; . This will delete the local copy of KV store .
2. Now start the splunk, Which will trigger the KV store resync operation automatically.
`./splunk start`

1. Check the KV store status again after few minutes and confirm that replicationstatus will be showing status as &quot;KV store captain&quot; or &quot;Non-captain KV store member&quot;

`./splunk show kvstore-status`

2. After completing Troubleshooting and resolving the problem, Then Engineer will move the HMAWI to &quot;Closed&quot; and inform the stake holder/creator with the evidence obtained on previous step through email cc&#39;ed Deloitte Health Monitoring DL: [**DT - Cyber Defense Engineering - Health Monitoring **](mailto:deloittesiemhealthmonitoringteam@deloitte.com) 
2. Additional Troubleshooting steps If Issue still exists:

In case, while performing the above troubleshooting steps if Engineer faces any restriction like permission related issue for enabling disabling acceleration reach out to the FC Engineering team for additional troubleshooting support.

If SIEM Engineering teams is unable to find root cause, then open Splunk Support case for further troubleshooting. When the solution is identified, Engineer updates the HMAWI to appropriate states (root cause identified, solution identified, solution implemented fields) on HMAWIs.

4. Then the Engineer moves HMAWI to closed column &amp; state and notifies SIEM Engineering team that issue has been resolved.