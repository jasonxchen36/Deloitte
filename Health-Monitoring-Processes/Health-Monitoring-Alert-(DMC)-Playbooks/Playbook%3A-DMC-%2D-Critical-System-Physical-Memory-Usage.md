- An alert from the Distributed Monitoring Console (DMC) is triggered due to the memory utilization on a Splunk server has breached its alert threshold in the last 5 minutes.
- Health Monitoring Alert Work Item (HMAWI) is automatically created by Azure Logic and added to HM team boards on the &quot;New&quot; column
  - HMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
- HM lead assign HMAWI work item to available HM member
  - HM lead is responsible for managing HM team member workload to make sure resolution can be met within SLA
- HM team member starts resolution process by following alert-specific playbook

#
# Playbook: DMC - Critical System Physical Memory Usage  

- Critical System Physical Memory Usage Playbook
  - HM team member moves HMAWI to &quot;Verification of Alert&quot; column on run team boards
  - HM team member SSH&#39;s to backend of host under question to verify accuracy of alert
   - If HMAWI is verified to be false positive, HM team member moves HMAWI to False Positive column &amp; state
  - HM team member runs the command to verify the current memory utilization is above 90%

    ``` free ``` 
``` free -t  (RAM + swap) ```


   - If memory utilization < 90%, alert is a false positive, HM team member moves HMAWI to &quot;False Positive&quot; column
    - If memory utilization is > 90%
      - HM team member runs the command

       ``` _ps -o pid,user,%mem,command ax | sort -b -k3 -r | head -n 10_``` 



      This will list the top 10 processes and the percentage of memory being consumed and by whom.
- Make note of the offending process(es)
  - If a Splunk related process is listed in the top 10 AND is consuming excessive (\&gt;20%) memory, restart Splunk.
    - Once Splunk has been restarted perform the above &#39;free&#39; command to ensure memory utilization is under breached threshold
  - If Splunk is NOT in the top 10 AND consuming excessive (\&gt;20%) memory alert HM Team with findings
  - Identify the oldest log files and remove it.
```du -shc * ```

- Additional Troubleshooting
  - If the above troubleshooting steps do not resolve the issue, contact the Engineering teams for troubleshooting assistance
    - HM team member updates root cause identified, solution identified, solution implemented fields on HMAWIs
    - HM team member moves HMAWI to closed column &amp; state
    - HM team member notifies HM team that issue has been resolved