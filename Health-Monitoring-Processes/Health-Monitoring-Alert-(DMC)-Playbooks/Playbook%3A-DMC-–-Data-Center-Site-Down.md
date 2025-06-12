
- An alert from the Distributed Monitoring Console (EMEA & AMER DMC) is triggered due to a substantial number of Splunk, or Splunk related, servers being unreachable.
- Health Monitoring Alert Work Item (HMAWI) is automatically created by Azure Logic and added to HM team boards on the &quot;New&quot; column
  - HMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
- HM leads assign HMAWI work item to available HM team member
  - HM lead is responsible for managing HM Team member workload to make sure resolution can be met within SLA.
- HM Team member starts resolution process by following alert-specific playbook

#Playbook: DMC – Data Center Site Down 
***Disabled in APAC***

- Data Center Site Down Playbook
  - HM Team member moves HMAWI to &quot;Verification of Alert&quot; column on HM team boards
  - HM Team member SSH&#39;s to the backend of the Distributed Monitoring Console (DMC) and attempts to telnet to the host reported as &quot;down&quot; by the alert over port 8089 using the command <pre><code> telnet <host> 8089 </code></pre>
    - If command prompt does not return, HM Team member should try to SSH directly into the host under question
      - HM Team membershould run the following command to ensure that the Splunk daemon is offline <pre><code> ps auxww | grep -i splunkd </code></pre>
        - If Splunk daemon is offline, HM Team member should run the command <pre><code> splunk start </code></pre>
      - If Splunk daemon is online, contact the GNOC to investigate the network connectivity between DMC and host under question
        - HM Team member moves HMAWI to &quot;Pending Stakeholder / On Hold&quot; column
        - If GNOC confirms it&#39;s a network connectivity issue, HM Team member moves HMAWI to &quot;Issue Identified&quot; column and documents root cause on HMAWI
        - Once GNOC restores network connectivity between hosts, HM Team member verifies the fix worked by attempting to telnet from the DMC to host under question using the command <pre><code> telnet <host> 8089 </code></pre>