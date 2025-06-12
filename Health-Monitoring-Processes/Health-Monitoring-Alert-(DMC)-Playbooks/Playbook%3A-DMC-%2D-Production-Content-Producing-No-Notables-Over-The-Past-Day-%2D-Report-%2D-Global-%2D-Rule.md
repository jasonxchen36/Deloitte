An alert from the Distributed Monitoring Console (DMC) is triggered when it is discovered that production content is producing no notables.

Health Monitoring Alert Work Item (DMAWI) is automatically created by Azure Logic and added to Run team boards on the &quot;New&quot; column.

DMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution.

Content assign DMAWI work item to available available Engineer.

Content Team is responsible for managing Engineer workload to make sure resolution can be met within SLA

Engineer starts resolution process by following alert-specific playbook

# 
# Playbook: DMC - Production Content Producing No Notables Over The Past Day - Report - Global - Rule

- SPM - Production Content Producing No Notables Over The Past Day - Report - Global – Rule Playbook
  - Engineer moves DMAWI to &quot;Verification of Alert&quot; column on run team boards
    - Engineer logs into user interface of a Splunk ES Search Head.
    - Perform the following search to verify:

      <pre><code> index=_internal sourcetype=scheduler savedsearch_name="*FC*" NOT savedsearch_name="*DEV*" | stats values(alert_actions) as alert_actions values(status) as status values(reason) as reason by savedsearch_name, _time| fields _time savedsearch_name status reason alert_actions </code></pre> 

        - If Notables are firing, investigate time frame alert reported no Notables.
     - If Notables are not being fired:
       - Verify Search Heads and Indexers are up and healthy. From any Production ES Search Head navigate to &quot;Settings -\&gt; Search Head Clustering&quot;
         - All Search Heads listed should show a Status of &quot;Up&quot; and have a recent heartbeat.
         - If any Search Heads or Indexers are down report to Health Monitoring team (deloittesiemhealthmonitoringteam@deloitte.com) to bring server/services back up.
       - Check the KV Store on Search Heads by logging in (SSH) to any ES Search Head and performing the following command:

          <pre><code>splunk show kvstore-status</code></pre>


  
        - Observe the status and replicationStatus fields to verify there are no errors.
           -    If status is not ready and/or replication is not occurring notify Health Monitoring team (deloittesiemhealthmonitoringteam@deloitte.com) to have the issue resolved.
       - Alternatively, the following search can be run to obtain the status of KV Stores:

         <pre><code> | rest splunk_server_group=dmc_group_kv_store splunk_server_group="dmc_searchheadclustergroup_AMEA_PROD_ES_SHC" /services/server/introspection/kvstore/serverstatus | eval Instance=splunk_server | spath input=data | eval hours=toString(round(uptime/3600, 2)) | rename repl.ismaster as rstate | rename repl.secondary as secondary | eval replstate=if(rstate=="true", "Primary", if(secondary=="true", "Secondary", "N/A")) | stats  first(hours) AS "Uptime (hours)"  first(replstate) AS "Replication Role" by Instance | search "Replication Role"="N/A" </code></pre>


  
    
          - If search returns results notify Health Monitoring team (deloittesiemhealthmonitoringteam@deloitte.com) to have the issue resolved.
       - Query for skipped searched or delegated remote searches that have errored out by performing the following search:

         <pre><code> index=_internal sourcetype=scheduler savedsearch_name="*FC*" status="skipped" OR status="delegated_remote_error" NOT savedsearch_name="*DEV*" | stats values(alert_actions) as alert_actions values(status) as status values(reason) as reason by savedsearch_name, _time | fields _time savedsearch_name status reason alert_actions </code></pre>


  
    
          - If search has been skipped or errored out share reason with Health Monitoring team (deloittesiemhealthmonitoringteam@deloitte.com) to have this resolved.
- Additional Troubleshooting
  - If the above troubleshooting steps do not resolve the issue, contact the FC Engineering teams for troubleshooting assistance
    - Engineer updates root cause identified, solution identified, solution implemented fields on DMAWIs
    - Engineer moves DMAWI to closed column &amp; state
    - Engineer notifies FC Engineering teams that issue has been resolved
    -  Engineer moves DMAWI to &quot;SOC Notification&quot; column and notifies the SOC they are free to re-run content over the time period where network connectivity was down
    - Identify affected log source by leveraging the following ADO query: [https://dev.azure.com/GlobalSOC/Splunk/\_queries/query/3117116b-fb2e-4b8c-b860-bdf88d34b6cd/](https://dev.azure.com/GlobalSOC/Splunk/_queries/query/3117116b-fb2e-4b8c-b860-bdf88d34b6cd/)
    - SOC re-runs content and verifies content has been populated
    - SOC notifies Engineer that content has been re-run
    -  Engineer moves DMAWI to &quot;Closed&quot; column.