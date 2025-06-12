
- An alert from the Search Head is triggered due to a Search, Alert, and Report being Auto Finalized.
- Search Performance Monitoring Alert Work Item (SPMAWI) is automatically created by Azure Logic and added to Health Monitoring Team board on the "New" column
- SPMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
- Health Monitoring team will assign SPMAWI work item to available team member.
- Health Monitoring team is responsible for managing  workload to make sure resolution can be met within SLA
- Health Monitoring team member starts resolution process by following alert-specific playbook.
# 
#Playbook: SPM - Delegated Remote Error Savedsearches 

- SPM -  Delegated Remote Error Savedsearches:
  
   The captain delegates the search to one search head, but suffers the error indicated by status=delegated_remote_error" in the first log message. Then, it delegates the search to a different search head. But the first search head also runs the search. This Potentially indicates the problem with the Search Head and or Search

- Health Monitoring team member moves SPMAWI to "Active" column on Health Monitoring Team board
- Health Monitoring team member accesses Splunk GUI and verifies the Search, Report, and Alert by running the same search provided below:

**To be run on SH**
       <pre><code> index=_internal sourcetype=scheduler status=delegated_remote_error retry=0 
| rex field=_raw "status=delegated_remote_error, (?<error_message>[^,]+)"
| eval Scheduled=strftime(scheduled_time, "%Y-%m-%d %H:%M:%S")
| stats values(Scheduled) as Scheduled values(status) as Status values(user) as User values(savedsearch_name) as Savedsearch_name values(error_message) as Reason by _time,savedsearch_name,host | sort - Scheduled | fields Scheduled host Status User Savedsearch_name Reason </code></pre>


 - After performing the above steps, the HM team member will follow the steps provided below:
 - Check the Reason of the search getting the error as per below screenshots:

![DRE_1.png](/.attachments/DRE_1-97dd26fa-60d7-4e03-838e-dce1af277999.png)![DRE_2.png](/.attachments/DRE_2-30b09cab-30f1-49b4-948d-2457898945e7.png)

- If the reason of the error is due to bad performance of Splunk Infrastructure, Create a ticket to Cyber Defense Engineering - Architecture team([dt-cyberdefenseengineering-architecture@deloitte.com](mailto:dt-cyberdefenseengineering-architecture@deloitte.com)
  - Work Item Type - Bug Fix
  - Area Path - Splunk\Global FC Engineering
- HM team will create another work item to Content team to rerun the the content against the searches. 
   - Work Item Type - Search Performance Monitoring
   - Area Path - Splunk\DT - Cyber Defense Engineering - Content Development
   - Title - HM: List of Alerts Needing Re-execution Due to Delegated Remote Error -<Date>

 - After completing triaging, Then HMteam member will move the SPMAWI to “Completed” and inform the stake holder/creator of the report through email cc’ed deloittesiemhealthmonitoringteam@deloitte.com 

- Additional Troubleshooting Tips
   - While performing the above troubleshooting steps if HM team member faces any restriction like permission related issue for enabling disabling acceleration reach out to the Cyber Defense Engineering - Architecture  team(dt-cyberdefenseengineering-architecture@deloitte.com) for additional troubleshooting support.
- If Engineering teams is unable to find root cause, then open Splunk Support case for further troubleshooting:
- HM team member updates root cause identified, solution identified, solution implemented fields on SPMAWIs
- HM team member moves SPMAWI to closed column & state.
- HM team member notifies Health Monitoring team that issue has been resolved.


