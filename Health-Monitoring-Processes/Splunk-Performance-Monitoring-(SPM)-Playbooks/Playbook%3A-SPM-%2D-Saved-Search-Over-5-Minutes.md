**Alert is Disabled**

- An alert from the Distributed Monitoring Console (DMC) is triggered due to a Search, Alert, and Report being Auto Finalized.
- Search Performance Monitoring Alert Work Item (SPMAWI) is automatically created by Azure Logic and added to Health Monitoring Team board on the "New" column.
- SPMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution.
- HM Team assign SPMAWI work item to available HM Team member.
- HM Team is responsible for managing HM Team member workload to make sure resolution can be met within SLA.
- HM Team member starts resolution process by following alert-specific playbook.
# 
#Playbook: SPM - Saved Search Over 5 Minutes 

- SPM -  Saved Search Over 5 Minutes:
   - SPM - Saved Search Over 5 minutes:
   	- HM Team member moves SPMAWI to "Active" column on Health Monitoring Team board
   - HM Team member accesses Splunk GUI and verifies the search/report Data model name by running the same search provided below:

AMER     
```
index=_internal sourcetype=scheduler status=success savedsearch_name="*_SEARCH NAME_*" (host=usatramekj001 OR host=usatramekj002 OR host=usatramekj003 OR host=usatramekj100 OR host=usatramekj101 OR host=usatramekj149 OR host=usatramekj150 OR host=usatramekj151 OR host=usatramekj152) 
| eval run_time=(run_time/60) 
| stats count avg(run_time) as avg_run min(run_time) as min_run max(run_time) as max_run values(host) as host by savedsearch_name,app,user 
| where avg_run>5 
| sort - avg_run 
| fields host savedsearch_name app user avg_run min_run max_run
```
EMEA
```
index=_internal sourcetype=scheduler status=success savedsearch_name="*_SEARCH NAME_*" (host=eu1436l012 OR host=eu1436l013 OR host=eu1436l014 OR host=eu1436l069 OR host=eu1436l070)
| eval run_time=(run_time/60) 
| stats count avg(run_time) as avg_run min(run_time) as min_run max(run_time) as max_run values(host) as host by savedsearch_name,app,user 
| where avg_run>5 
| sort - avg_run 
| fields host savedsearch_name app user avg_run min_run max_run
```
APAC
```
index=_internal sourcetype=scheduler status=success savedsearch_name="*_SEARCH NAME_*" (host=ap1436l012 OR host=ap1436l013 OR host=ap1436l014 OR host=ap1436l069 OR host=ap1436l070)
| eval run_time=(run_time/60) 
| stats count avg(run_time) as avg_run min(run_time) as min_run max(run_time) as max_run values(host) as host by savedsearch_name,app,user 
| where avg_run>5 
| sort - avg_run 
| fields host savedsearch_name app user avg_run min_run max_run
```

  - After performing the above steps Health Monitoring team will follow the steps provided below: 
     - Check Cron schedule for the search. To see all the other searches ran at the same time (in the same Clock time). Also check the cron schedule document on the WIKI [here](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/153/Use-Case-Cron-Schedule).  

     - If this is the case, if you see many searches are scheduled to run at the same time, obviously memory consumption will hike resulting in the alert. In case, if you see so, Inform the content team to reschedule the searches in different timings with time difference of at least 5 Min in between.

     - Check the Search head memory, Login in to the backend of the Search head and use the command “free -m” to see the memory available in the search head and if the memory seems very high, Kill the appropriate Non-important processes that is consuming more memory. **Be very cautious while  killing the genuine processes and Non-important processes.** It is advisable to reach out seniors in case.

     - After completing Troubleshooting and resolving the problem, Then Run team engineer will move the SPMAWI to “Completed” and inform the stake holder/creator of the report through cc’ed deloittesiemhealthmonitoringteam@deloitte.com 


- Additional Troubleshooting Tips
    - While performing the above troubleshooting steps if HM Team member faces any restriction like permission related issue for enabling disabling acceleration reach out to the SIEM Engineering team for additional troubleshooting support.
     
      If SIEM Engineering teams is unable to find root cause, then open Splunk Support case for further troubleshooting:
        - HM team updates root cause identified, solution identified, solution implemented fields on SPMAWIs
        - HM team moves SPMAWI to closed column & state
        - HM team notifies HM team that issue has been resolved
