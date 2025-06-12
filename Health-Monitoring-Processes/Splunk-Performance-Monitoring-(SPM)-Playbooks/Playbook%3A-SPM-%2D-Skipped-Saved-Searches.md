

- An alert from the Distributed Monitoring Console (DMC) is triggered due to a Search, Alert, and Report being Auto Finalized.
- Search Performance Monitoring Alert Work Item (SPMAWI) is automatically created by Azure Logic and added to Health Monitoring board on the "New" column
- SPMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
- HM Team will assign SPMAWI work item to available Team member
- HM Team is responsible for managing the workload to make sure resolution can be met within SLA
HM team member starts resolution process by following alert-specific playbook
# 
#Playbook: SPM - Skipped Saved Searches 

- SPM -  Skipped Saved Searches:

- HM Team member moves SPMAWI to "Active" 
- HM Team member accesses Splunk GUI and verifies the search/report Data model name by running the same search provided below:
AMER


AMER
```  
index=_internal sourcetype=scheduler AND savedsearch_name="*_SEARCH NAME_*"
(host=usatramekj001 OR host=usatramekj002 OR host=usatramekj003 OR host=usatramekj100 OR host=usatramekj101 OR host=usatramekj149 OR host=usatramekj150 OR host=usatramekj151 OR host=usatramekj152) 
| eval Scheduled=strftime(scheduled_time, "%Y-%m-%d %H:%M:%S") | sort -Scheduled 
| table Scheduled user savedsearch_name status reason scheduled_time run_time result_count
```
EMEA
```  
index=_internal sourcetype=scheduler AND savedsearch_name="*_SEARCH NAME_*"
(host=eu1436l012 OR host=eu1436l013 OR host=eu1436l014 OR host=eu1436l069 OR host=eu1436l070)
| eval Scheduled=strftime(scheduled_time, "%Y-%m-%d %H:%M:%S") | sort -Scheduled 
| table Scheduled user savedsearch_name status reason scheduled_time run_time result_count
```
APAC
```  
index=_internal sourcetype=scheduler AND savedsearch_name="*_SEARCH NAME_*"
(host=ap1436l012 OR host=ap1436l013 OR host=ap1436l014 OR host=ap1436l069 OR host=ap1436l070)
| eval Scheduled=strftime(scheduled_time, "%Y-%m-%d %H:%M:%S") | sort -Scheduled 
| table Scheduled user savedsearch_name status reason scheduled_time run_time result_count
```
  - See the field “reason” for appropriate saved search filtering with field “savedsearch_name” why the searches are getting skipped.

  - After performing the above steps HM Team member will follow the steps provided below:
     - If the reason looks like below
![saved searches 1.png](/.attachments/saved%20searches%201-1065ba2e-c253-4fae-8035-398825c1ebf4.png)
       the search specifies a macro <Macro_Name> that may not be visible / accessible by the user running the search due to insufficient permissions. Also, the macro name could be misspelled, or user does not have "read" permission for the macro, or the macro has not been shared with this application. Click Settings, Advanced search, Search Macros to view macro information.

     - If the Reason looks like below
![saved searches 2.png](/.attachments/saved%20searches%202-5fc4d81b-c107-4a56-b30f-68999a179b11.png)
     it can generally be considered a false positive. Verify if the search ran recently (after the alert time). Go to (Settings -> Searches & Reports -> Search with the Saved_search name -> View recent). If so, then run team engineer will move the SPMAWI to “Closed” column.

     - If the reason looks like below
![saved searches 3.png](/.attachments/saved%20searches%203-9ba222ba-eed1-48c2-923c-6d30179414ae.png)
     the user is not allowed to run the saved search. Check the user that is running the search. Check the permissions of the user/if the user has the permissions to do the search. 

     - If the reason looks like below
![saved searches 4.png](/.attachments/saved%20searches%204-9633ff6a-eafc-415a-be46-758911058852.png)
     the search is missing a command. Check if the Search, Report, Alert, and query is running fine or having an error. Contact Build & Run content team to review the search in case.

     - After completing Troubleshooting and resolving the problem, Then HM Team member will move the SPMAWI to “Completed” and inform the stake holder/creator of the report through email cc’ed deloittesiemhealthmonitoringteam@deloitte.com  

- Additional Troubleshooting Tips
    - • While performing the above troubleshooting steps if HM Team member faces any restriction like permission related issue for enabling disabling acceleration reach out to the HM team for additional troubleshooting support.

- If HM Team is unable to find root cause, then open Splunk Support case for further troubleshooting:
- HM Team member updates root cause identified, solution identified, solution implemented fields on SPMAWIs
- HM Team member moves SPMAWI to closed column & state
- HM Team member notifies HM team that issue has been resolved.