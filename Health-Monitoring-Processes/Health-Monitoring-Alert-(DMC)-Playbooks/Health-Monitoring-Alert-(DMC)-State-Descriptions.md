The following defines the FC Engineering team board descriptions and their associated states:

An alert from the Distributed Monitoring Console (DMC) is triggered 

##New
- Health Monitoring Alert Work Item (HMAWI) is automatically created by Azure Logic and added to Run team boards on the "New" column
- HMAWI is automatically assigned to run team lead
- Run team lead assigns HMAWI to available run engineer based on engineer work load to make sure resolution can be met within SLA
- Once Engineer is assigned, Engineer moves HMAWI board/state to Verification of Alert


##Verification of Alert
- This board column intends to hold HMAWIs that are currently being verified as not a false positive. Alert is determined to be valid if there is no data present in index for the past 24 hours, or a significant drop in event volume
- If alert is determined to be false positive, engineer move HMAWI to False Positive Column
- If alert is determined to be valid, engineer moves HMAWI to Active column

##False Positive
- This column is intended to hold HMAWIs that have been determined as false positives during the Verification of Alert state / column
- Update HMAWI with the reason this alert fired as a false positive and engage the health monitoring team to implement tuning

##Duplicate
- THis column is intended to hold HMAWIs that have been identified as duplicates of other HMAWIs
- Engineer should link the duplicate HMAWI to the original HMAWI and document on duplicate work item which HMAWI holds the master tracking

##Active 
- Engineer begins investigation of why index is missing data by following playbook here
- Engineer updates the "Comments" column on Index_Mapping.csv via the lookup editor on the ES SHC
- If root cause is identified, engineer documents root cause on "Root Cause Identified" field of HMAWI
--**Engineer moves HMAWI to Issue Identified state / column
--**If engineer is waiting on stakeholder or data source owner engineer moves HMAWI to Pending Stakeholder / On hold column

##Pending Stakeholder / On Hold
- This board column / state is intended to hold HMAWIs where clarification from a stakeholder or data source owner is needed to proceed with investigation
- Engineer documents status of why HMAWI is on hold in discussion column
- Once appropriate communication has been received from stakeholder or data source owner, engineer moves HMAWI to Active board column / state

##Issue Identified
- Engineer documents root cause on HMAWI
- Engineer works to identify a solution to root cause
- Once solution is identified, engineer documents proposed solution on the Solution Identified field of the HMAWI
- Engineer moves HMAWI to Solution Identified board column / state

##Solution Identified
- Engineer works to implement identified solution
-- If changes are not working, troubleshoot with deployment Engineers 
-- If solution requires reaching out to data source owner or stakeholder, engineer moves HMAWI to Pending Stakeholder / on Hold column
-- If this fails, engineer works with run team lead to open a Splunk support case for further troubleshooting; engineer moves HMAWI to Pending Stakeholder / on Hold column
- If solution is identified to work, engineer creates PR to fix the applicable problem. Once PR is merged into the cluster, engineer moves HMAWI to Solution Implemented column

##Solution Implemented
- This column / board state is intended to hold HMAWIs where the solution has been implemented and verified to work 
- If solution is verified to work with all data back into the problem index, engineer moves HMAWI to Data Restored column

##Data Restored
- Engineer verifies with Global FC Engineering team that the changes are accurate/expected 
-- If changes are not working, troubleshoot with deployment Engineers and move HMAWI back to Active column / board state
-- If changes restore data, engineer documents the solution implemented on field "Solution Implemented" on HMAWI
- If changes are confirmed accurate/expected, run engineer moves HMAWI to SOC Notification column
##SOC Notification
- This column is intended to hold HMAWIs where all of the data is restored and ready for the SOC to be notified of the same
- SOC should be notified (DeloitteGTSSOCALL@deloitte.com) that data is back in index, and they are free to re-run content over period where data was gone. 
-- [Automated Dashboard for Missing SNOW Tickets](/Content-Development-Processes/Dashboards/Automated-Dashboard-for-Missing-SNOW-Tickets). This step is automated by way of a saved search running hourly on the DMC. The saved search will email the SOC DL defined above, as well as the engineer assigned to the ticket.
- Once SOC has re-run content, SOC must coordinate with engineer assigned to the ticket and let engineer know when it is safe to close the ticket
- Until this coordination happens, SOC may receive duplicate emails for the same ticket.

#Closed
- Final state, HMAWI is completed by setting state to Closed and changes are in production
