- An alert from the AMER SHC is triggered due to an empty lookup table. This lookup should be re-populated at the earliest convenience.
- Search Performance Monitoring Alert Work Item (SPMAWI) is automatically created by Azure Logic and added to o Health Monitoring Team board on the "New" column. Also, an email is sent to deloittesiemhealthmonitoringteam@deloitte.com
-  SPMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
- Health Monitoring Team will assign SPMAWI work item to available Team member.
- Health Monitoring Team is responsible for managing workload among the resources to make sure resolution can be met within SLA
Health Monitoring Team starts resolution process by following alert-specific playbook 
# 
#Playbook: SPM - Missing Lookup Value
- SPM - Missing Lookup Value
 - Health Monitoring Team member moves SPMAWI to "Active" 
- Health Monitoring Team member accesses Splunk GUI and verifies the veracity of the triggered alert by running the following query and checking if results are the same as the received on the SPMAWI:
      <pre><code>| rest /services/data/lookup-table-files | search eai:acl.app="DA-ESS-*-Lookups" | table title | map maxsearches=99999 search="| inputlookup $title$ | stats count | eval title=\"$title$\" | table count title" | rename count as lookup_table_entries, title as lookup | search lookup_table_entries=0 | table lookup lookup_table_entries </code></pre>
-    When finished with the above steps, Health Monitoring Team member will follow the steps provided:
        
 - If there are no empty lookup tables, change the status to False Positive
  - If there are empty lookup tables, check to see when the lookup was last edited, and see who edited that lookup with the below query:
           <pre><code>index=_internal "Lookup edited successfully" lookup_file="$lookup_name$" | table _time user namespace lookup_file</code></pre>
      - If a user edited the lookup within the last 7 days, reach out to that person to see why they did it, and let them know that it is blank
      - If the lookup has not been edited manually, check to see if lookup is being populated by an outputlookup command within a saved search
          - Go to settings, then “Searches, reports, and alerts”
          - Switch App: to All and then type outputlookup $lookup_name within the search bar
             ![SPM Missing Lookup Value 1.png](/.attachments/SPM%20Missing%20Lookup%20Value%201-d1a153e8-856c-48b6-8403-094f1916d90a.png)
        - If it is, check to see if there are issues as to why the search is not populated the lookup properly. Issues include breaks in CIM compliance, no results, etc
       - If the above 3 steps do not apply, reach out to the owner of the lookup/Content Team to see if they accidently uploaded a blank lookup table.
	   - If lookup table is blank and this is expected (requested from the stakeholder), please add “-“ into the cells.

