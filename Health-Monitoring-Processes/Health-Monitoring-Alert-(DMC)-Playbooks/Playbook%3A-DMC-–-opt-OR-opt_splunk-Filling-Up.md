• An alert from the Distributed Monitoring Console (DMC) is triggered due a host that is expected to report into the License Master but has not in the last 5 minutes

• Health Monitoring Alert Work Item (HMAWI) is automatically created by Azure Logic and added to Health Monitoring team boards on the "New" column.

• HMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution.

• Health Monitoring team assign HMAWI work item to available team member.

• Health Monitoring team is responsible for managing team member workload to make sure resolution can be met within SLA.

Health monitoring team member starts resolution process by following alert-specific playbook.

#Playbook: DMC – /opt/\* OR /opt/splunk/\* filling up 

- /opt/\* OR /opt/splunk/\* Filling Up Playbook
  - Health Monitoring team member moves HMAWI to &quot;Verification of Alert&quot; column on run team boards
  - Health Monitoring team member SSH&#39;s to backend of host under question to verify accuracy of alert
    - If HMAWI is verified to be false positive, Health Monitoring team member moves HMAWI to False Positive column &amp; state
  - Health Monitoring team member runs the command <pre><code>_df -h_</code></pre> to verify mount point &quot;/opt/splunk/\*&quot; is >= 95% capacity
    - If host mount point &quot;/opt/\*&quot; OR "/opt/splunk/\*&quot; is < 95% full, alert is a false positive, Health Monitoring team member moves HMAWI to &quot;False Positive&quot; column
    - If host mount point &quot;/opt/\*&quot; OR &quot;/opt/splunk/\*&quot; is >= 95% full
      - If host under question is a Splunk indexer or a Splunk Heavy Forwarder:
        - Navigate to /opt/splunk/var/run/searchpeers
        - Sort the files (search bundles) in this directory chronologically using the command <pre><code>_ls -alt_ </code></pre>
        - Delete largest search bundles that are older than 24 hours
        - If it is a production indexer, open an ERFC to restart Splunk at earliest availability
        - If it is not a production indexer, restart Splunk

     - If the host under question is a Splunk Search Head
       - Navigate to &quot;/opt/splunk/var/run/searchpeers&quot;
       - Sort files in this directory chronologically _ls -alt_
       - Delete largest files in this directory that are older than 24 hours
       - If the host in question is a production Search Head, open an ERFC to restart Splunk at earliest availability
      - If it is not a production Search Head, restart Splunk
- Additional Troubleshooting
  -  If the above troubleshooting steps do not resolve the issue, contact the Cyber Defense Engineering - Health Monitoring  - deloittesiemhealthmonitoringteam@deloitte.com for troubleshooting assistance.
    - Health Monitoring team member updates root cause identified, solution identified, solution implemented fields on HMAWIs.
    - Health Monitoring team member moves HMAWI to closed column &amp; state.
    - Health Monitoring team member notifies Architecture Team that issue has been resolved.