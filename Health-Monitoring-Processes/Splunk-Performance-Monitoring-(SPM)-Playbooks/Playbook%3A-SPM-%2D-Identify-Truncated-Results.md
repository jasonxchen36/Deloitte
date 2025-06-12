**Alert is disabled**
- An alert from the Distributed Monitoring Console (DMC) is triggered due to a Search, Alert, and Report being Auto Finalized.
- Search Performance Monitoring Alert Work Item (SPMAWI) is automatically created by Azure Logic and added to Health Monitoring Team board on the "New" column
- SPMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
- HM Team will assign SPMAWI work item to available team member 
- HM Team is responsible for managing Run Engineer workload to make sure resolution can be met within SLA
- HM Team will starts resolution process by following alert-specific playbook
# 
#Playbook: SPM - Identify Truncated Results 

- SPM -  Identify Truncated Results:
    - SPM - Identify truncated results:
    - HM Team moves SPMAWI to "Active" column on Health Monitoring Team board
    - HM Team member accesses Splunk GUI and verifies the search/report Data model name by running the same search provided below:
- AMER
      <pre><code> | rest /services/search/jobs | eval position=mvfind(searchProviders, "amea_prod_es_shc_\w+") | eval "Search Provider"=mvindex(searchProviders,position) | search "Search Provider"="amea_prod_es_shc_usatramekj001" OR "Search Provider"="amea_prod_es_shc_usatramekj002" OR "Search Provider"="amea_prod_es_shc_usatramekj003" OR "Search Provider"="amea_prod_es_shc_usatramekj101" OR "Search Provider"="amea_prod_es_shc_usatramekj100" | search messages.fatal="Search auto-canceled" | rename author as user, title as "splunk search query",  sid as "Search Job ID", earliestTime as "Job start time", runDuration as "duration(seconds)", splunk_server as "splunk server" messages.fatal as message | fields user, "splunk search query", "Search Job ID", "message", "Job start time", duration(seconds),"splunk server" "Search Provider" </code></pre>

- EMEA
     
       <pre><code> | rest /services/search/jobs | eval position=mvfind(searchProviders, "emea_prod_es_sh_\w+") | eval "Search Provider"=mvindex(searchProviders,position) | search "Search Provider"="emea_prod_es_sh_EU1436L012" OR "Search Provider"="emea_prod_es_sh_EU1436L013" OR  "Search Provider"="emea_prod_es_sh_EU1436L014" OR "Search Provider"="emea_prod_es_sh_EU1436L069" OR "Search Provider"="emea_prod_es_sh_EU1436L070" | search messages.fatal="Search auto-canceled" | rename author as user, title as "splunk search query",  sid as "Search Job ID", earliestTime as "Job start time", runDuration as "duration(seconds)", splunk_server as "splunk server" messages.fatal as message | fields user, "splunk search query", "Search Job ID", "message", "Job start time", duration(seconds),"splunk server" "Search Provider" </code></pre>

- APAC
<pre><code> | rest /services/search/jobs | eval position=mvfind(searchProviders, "apac_prod_es_sh_\w+") | eval "Search Provider"=mvindex(searchProviders,position) | search "Search Provider"="amea_prod_es_shc_AP1436L012" OR "Search Provider"="amea_prod_es_shc_AP1436L013" OR "Search Provider"="amea_prod_es_shc_AP1436L014" OR "Search Provider"="amea_prod_es_shc_AP1436L069" OR "Search Provider"="amea_prod_es_shc_AP1436L070" | search messages.fatal="Search auto-canceled" | rename author as user, title as "splunk search query",  sid as "Search Job ID", earliestTime as "Job start time", runDuration as "duration(seconds)", splunk_server as "splunk server" messages.fatal as message | fields user, "splunk search query", "Search Job ID", "message", "Job start time", duration(seconds),"splunk server" "Search Provider" </code></pre>

   - After performing the above steps HM team member will follow the steps provided below:
      - Check if the Search, Report, Alert is efficient, and query is running fine or having an error. Contact owner of the alert to review the search in case.
      - Check the Duration, how much time did the search took to run. If it is High, contact owner of the alert to review the search in case.
      - • Try to copy the search and run in the same search head where the alert generated. If you don’t see any errors, please change the state as “closed” as this is False Positive.
      - But If you still don’t see completing successfully, Click on the Icon right before your username.
![truncated 1.png](/.attachments/truncated%201-40d6c2b1-de6b-4ac4-94ac-e6a5b290f67c.png)
      - Check if there is any problem with Index Processor, Indexer Clustering & Search head Clustering. (It should be indicated in Red Marks). If so, Inform SIEM Engineering Team about it.
![truncated 2.png](/.attachments/truncated%202-c0d044eb-ab16-423d-882c-c67aa6e7280f.png)
      - Also, check to see if there are any errors like this. If so, Inform the  SIEM Engineering Team about it.
![truncated 3.png](/.attachments/truncated%203-740e404c-ce6c-4bf6-b56b-cc1167a77fc9.png)
      - Check if many searches are scheduled to run at the same time, obviously memory consumption will hike resulting in the alert. In case, If you see so, Inform the alert owner to reschedule the searches in different timings with time difference of at least 5 Min in between.

      - Check the Search head memory (Login to the search head, Where the search has ran), Login in to the backend of the Search head and use the command “free -m” to see the memory available in the search head and if the memory seems very high, Kill the appropriate Non-important processes that is consuming more memory. Be very cautious while killing the genuine processes and Non-important processes. It is advisable to reach out seniors in case.

      - After completing Troubleshooting and resolving the problem, Then HM team member  will move the SPMAWI to “Completed” and inform the stake holder/creator of the report through email cc’ed   deloittesiemhealthmonitoringteam@deloitte.com  

- Additional Troubleshooting Tips
    - While performing the above troubleshooting steps if HM team member faces any restriction like permission related issue for enabling disabling acceleration reach out to the SIEM Engineering team for additional troubleshooting support.
     
      If Health Monitoring team is unable to find root cause, then open Splunk Support case for further troubleshooting:
        - HM team member updates root cause identified, solution identified, solution implemented fields on SPMAWIs
        - HM team member SPMAWI to closed column & state
        - HM team member notifies Team that issue has been resolved.

