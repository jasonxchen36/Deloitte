An alert from the Distributed Monitoring Console (DMC) is triggered when a production Search Head returns a status of &quot;down&quot;.

Health Monitoring Alert Work Item (HMAWI) is automatically created by Azure Logic and added to HM team boards on the &quot;New&quot; column

 HMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution

HM team assign HMAWI work item to available HM team member

HM team is responsible for managing HM team member work load to make sure resolution can be met within SLA

HM team starts resolution process by following alert-specific playbook

# 
# Playbook: DMC – SH Not Reachable

- SH Not Reachable Playbook
  - HM team member moves HMAWI to &quot;Verification of Alert&quot; column on HM team boards
  - HM team member SSH&#39;s to the backend of the Distributed Monitoring Console (DMC) and attempts to telnet to the host reported as &quot;down&quot; by the alert over port 8089 using the command
        <pre><code> telnet <host> 8089 </code></pre>


   - If command prompt does not return, HM team member should try to SSH directly into the host under question
   - HM team member should run the following command to ensure that the Splunk daemon is offline<pre> <code> ps auxww | grep -i splunkd </code></pre>
  - If Splunk daemon is offline, HM team member should run the command
            <pre><code>   splunk start </code></pre>


   - If Splunk daemon is online, contact the GNOC to investigate the network connectivity between DMC and host under question
  - HM team member moves HMAWI to &quot;Pending Stakeholder / On Hold&quot; column
  - If GNOC confirms it&#39;s a network connectivity issue, HM team member moves HMAWI to &quot;Issue Identified&quot; column and documents root cause on HMAWI
   - Once GNOC restores network connectivity between hosts, HM team member verifies the fix worked by attempting to telnet from the DMC to host under question using the command
                        <pre><code> telnet <host> 8089 </code></pre>


    - If the command succeeds, the HM team member verifies the Search Head is up by:
      - From any Production ES Search Head navigate to “Settings -> Search Head Clustering”
      - Check that the Search Head in question is listed and shows a Status of “Up” and has a recent heartbeat
      - If HMAWI is verified to be false positive, engineer moves HMAWI to False Positive column &amp; state

- Additional Troubleshooting
  - If the above troubleshooting steps do not resolve the issue, contact the Architecture team for troubleshooting assistance
    - HM team member updates root cause identified, solution identified, solution implemented fields on HMAWIs
    - HM team member moves HMAWI to closed column &amp; state
    - HM team member notifies HM team that issue has been resolved
