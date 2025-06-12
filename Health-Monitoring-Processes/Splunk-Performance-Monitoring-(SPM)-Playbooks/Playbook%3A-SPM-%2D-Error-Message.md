
- An alert from the Distributed Monitoring Console (DMC) is triggered due to a Search, Alert, and Report being Auto Finalized.
- Search Performance Monitoring Alert Work Item (SPMAWI) is automatically created by Azure Logic and added to Health Monitoring Team board on the "New" column
- SPMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
- HM Team assign SPMAWI work item to available HM Team member
- HM Team is responsible for managing HM Team member workload to make sure resolution can be met within SLA
- HM Team member starts resolution process by following alert-specific playbook
# 
#Playbook: SPM - Error Message 

- SPM -  Error Message:
 - HM Team member moves SPMAWI to "Active" column on Health Monitoring Team board
  - HM Team member accesses Splunk GUI and verifies the search/report Data model name by running the same search provided below:
  
**AMER**
```
index=_internal sourcetype=scheduler AND savedsearch_name="*FC*" 
| search NOT (errmsg="*The search job terminated unexpectedly*" 
OR errmsg="*peer went down*" OR errmsg="*Error decompressing zstd block: Destination buffer is too small*" 
OR errmsg="*Unable to read the job status.*"  
OR errmsg="*Error in 'DispatchManager': The user 'splunk-system-user' does not have sufficient search privileges.*") 
| search host=usatramekj001 OR host=usatramekj002 OR host=usatramekj003 OR host=usatramekj100 OR host=usatramekj101 
| stats  values(errmsg) as errmsg count(_time) as error_count values(host) as host by savedsearch_name 
| fields savedsearch_name errmsg error_count host
```
**EMEA**
```
index=_internal sourcetype=scheduler AND savedsearch_name="*FC*" 
| search NOT (errmsg="*The search job terminated unexpectedly*" OR errmsg="*peer went down*" OR errmsg="*Error decompressing zstd block: Destination buffer is too small*" 
OR errmsg="*Unable to read the job status.*"  
OR errmsg="*Error in 'DispatchManager': The user 'splunk-system-user' does not have sufficient search privileges.*") 
| search host= EU1436L012 OR host = EU1436L013 OR host = EU1436L014 OR host= EU1436L069 OR host = EU1436L070 
| stats  values(errmsg) as errmsg count(_time) as error_count values(host) as host by savedsearch_name 
| fields savedsearch_name errmsg error_count host
```
**APAC**
```
index=_internal sourcetype=scheduler AND savedsearch_name="*FC*" 
| search NOT (errmsg="*The search job terminated unexpectedly*" OR errmsg="*peer went down*" OR errmsg="*Error decompressing zstd block: Destination buffer is too small*" 
OR errmsg="*Unable to read the job status.*"  
OR errmsg="*Error in 'DispatchManager': The user 'splunk-system-user' does not have sufficient search privileges.*") 
| search host = AP1436L012 OR host = AP1436L013 OR host =AP1436L014 OR host = AP1436L069 OR host =AP1436L070 
| stats  values(errmsg) as errmsg count(_time) as error_count values(host) as host by savedsearch_name 
| fields savedsearch_name errmsg error_count host
```
   - After performing the above steps Health Monitoring team will follow the steps provided below:
     - Check the “errmsg”. This would be self-explanatory.
![error 1.png](/.attachments/error%201-920dc92c-2862-4a64-997b-c64fcbc67b85.png)
     - Check for the alerts where the value for “error_count” is double digit or more.
![error 2.png](/.attachments/error%202-30b65b43-d242-45c5-b348-dc0964e21cd0.png)
     - Check the “errmsg” to find the root cause for the error with the alert (savedsearch_name). This should be Self-Explanatory. 

     - Investigate more about the errmsg if the problem is with the Lookup involved with the query or If the problem is with user which is running the search doesn’t have enough privileges to run the search.

     - Or Check if the problem is with the query itself. Investigate and inform the Content team to resolve the issue further related to the Saved searches accordingly.

     - After completing Troubleshooting and resolving the problem, Then Health Monitoring team member will move the SPMAWI to “Completed” and inform the stake holder/creator of the report through email cc’ed deloittesiemhealthmonitoringteam@deloitte.com  

- Additional Troubleshooting Tips
    - While performing the above troubleshooting steps if HM Team member faces any restriction like permission related issue for enabling disabling acceleration reach out to the SIEM Engineering team for additional troubleshooting support.
     
      If Engineering team is unable to find root cause, then open Splunk Support case for further troubleshooting:
        - HM team member updates root cause identified, solution identified, solution implemented fields on SPMAWIs.
        - HM team member moves SPMAWI to closed column & state.
        - HM team member Team that issue has been resolved.
