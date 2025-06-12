The following defines the CIM Normalization team board descriptions and their associated states:
 
##Not Assigned
- CIM Validation Request WI (CVRWI) has not been assigned to an Engineer
- Global FC Engineering leads assign CVRWI to Engineer based on Engineer's data source experience and current workload
- CVRWI's with "Urgent" tag should be assigned as soon as possible and moved to Urgent WIP board/state
- Once Engineer is assigned, Engineer moves CVRWI board/state to New data source - Review with Content or WIP


##On Hold
- CVRWI is on hold until on hold reason can be resolved (e.g., Splunk bug, hold on data source ingestion)
- Once on hold reason is resolved, CVRWI board/state is moved to New data source - Review with Content or WIP

##New data source - Review with Content
Note: This includes existing data source types from new sources (e.g., WinEventLog from MF that hasn't been ingested yet). Skip this board/state if change requested affects a data source that exists in Splunk - board/state should be switched from Not Assigned to WIP. 

- Review raw data within regional Splunk Dev environment with the Global FC Engineering Content team
- Update CVRWI with Global FC Engineering Content team feedback (which datamodel, etc.)
- Update CVRWI board/state to WIP

##Work in Progress (WIP)
- Engineer creates/updates eventtypes.conf, tags.conf, and props.conf with requested changes from CVRWI
- Engineer pushes changes to .conf files to standalone SH for testing eventtypes, tags, and fields (CIM app is not on standalone so no need to push macros.conf in this state)
- Engineer verifies with Global FC Engineering Content team changes on standalone SH, if changes are confirmed, move CVRWI to Ready for Stage Test board/state


##Ready for Stage Test
- Engineer creates PR for regional Staging SHC using the changes verified on the standalone 
--**For data in new indexes, Engineer adds new index name to the appropriate Data Model macro in Splunk_SA_CIM/local/macros.conf - this should be done in the same PR
- Once PR is approved and pushed to Staging SHC, move CVRWI board/state to Stage Test
####***How to Verify Changes with Global FC Engineering Content Team***
- Refer to Verify Changes Process within this wiki
- If Verify Changes Process does not work or Engineer is unsure about results, schedule a call with Engineer on Global FC Engineering Content team

##Stage Test
- Engineer verifies with Global FC Engineering Content team that the changes are accurate/expected in Staging SHC (make sure to check pivot table results or DM search results as well as raw data changes)
-- If changes are not working, troubleshoot with deployment Engineers
- If changes are confirmed accurate/expected by the Global FC Engineering Content team, move CVRWI board/state to Ready for Production

##Ready for Production
- Engineer creates PR for regional Production ES SHC using the changes verified on Staging SHC 
--**For data in new indexes, Engineer adds new index name to the appropriate Data Model macro in Splunk_SA_CIM/local/macros.conf - this should be done in the same PR
- Once PR is approved and pushed to Production ES SHC, move CVRWI board/state to Ready For Prod Verification

##Ready for Prod Verification
- Engineer verifies with Global FC Engineering Content team that the changes are accurate/expected in Production ES SHC (make sure to check pivot table results or DM search results as well as raw data changes)
-- If changes are not working, troubleshoot with deployment Engineers
- If changes are confirmed accurate/expected by the Global FC Engineering Content team, move CVRWI to Verified board and state to Closed

#Verified
- Final state, CVRWI is completed by setting state to Closed and changes are in production
