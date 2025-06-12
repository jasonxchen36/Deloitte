**##Ready to be Worked On Board**
 

1. Reviewed requirements with stakeholders during “Bi-weekly content development pipeline 
        review”. Point of this meeting is to have stakeholders align on monitoring logic intent and 
        clear any ambiguity they may have before it is developed
1. Tag the work item with “Reviewed”
1. Build Priority is defined
1. Region is defined
1. Title should be less than 100 characters to avoid enabling /disabling errors in Splunk
1. Description (also known as requirements) are clearly defined
1. Content Title is aligned to the FC use case framework
1. Build Content State should equal “New”


**##WIP Board**
1. SOP Development work item created
1. SOP Dev work item has the same title as Build Content Work Item
1. SOP Dev work item is linked as “Related work” to Build Content Work Item
1. Boolean checklist on Build Content Work Item set to True after SOP Dev work item is created
1. Project S Team begins development
1. If the content item is being developed by a Member Firm content developer, it should be tagged with "<MF> Content Developer" (for example, "United States Content Developer") and reside in the "Member Firm Content Developer" swim lane during development



**##	Pending CIM Board**
1. If data needed to properly implement content is not CIM validated (also known as normalized), a CIM Validation work item is opened describing the support needed from the Deployment Team in order to get data set normalized / CIM validated

2. If there is a CIM validation work item opened, it should be linked to the Build Content Work Item it supports as “Related Work” 

1. Build Content Work Items that are pending supporting implementation from Deployment team live on the Pending CIM board until their respective CIM work items are implemented in our Staging environment
1. Build Content State should equal “Pending CIM”

1. Build content work items live on the WIP board until all applicable documentation fields (on the work item) are filled out (E.g. search runtime, SecOps parameters, notable parameters)
1. Build content state should equal “WIP”




**##GEMS Eng Review Board**

1. After development is complete and all documentation is filled out on the Build Content Work Item, Build Content Work Items should be moved to this board in preparation for our internal project s review meeting (currently held on Thursdays)
1. If there are (major) logic adjustments to make to the correlation search query, the build content work item should be moved back to the WIP board and re-reviewed with the internal project S team
1. By the time a work item reaches Project S Review, it must be filled out with "Ingested Log Source" and "Required Logging" data. 
   - Write all of this in SPL-friendly format, and assume an “AND” statement between necessary index(es) and required logging
   - For example, if an authentication alert requires successful Windows Event Logs and Azure AD logs, Ingested Log Source / Required Logging should contain the following values:
                                                               i.      Ingested Log Source: index=”<mf>_endpoint_microsoft_windows_security” OR index=”all_cloud_microsoft_aad”
                                                             ii.      Required Logging: signature_id=”4624” OR signature_id=”0” (Azure AD successful Authentication ID)
                                                           iii.      In Splunk, these conditions will translate to (index=”<mf>_endpoint_microsoft_windows_security” OR index=”all_cloud_microsoft_aad”) AND (signature_id=”4624” OR signature_id=”0”)
1. Build Content state should equal “Project S Review”




**##SOC Review Board**

1. Build content items should only be moved to this board after they have been reviewed by the project s build content development team
2. This column is for content items that must be preliminarily reviewed by the SOC before being moved to Volume Testing
3. Content team creates a Content Feedback Work Item in the Global FC Monitoring area path
    _Note: If you are a MF Content Developer, please tag your Content Feedback Items with "United States Content Developer"_
4. Content team emails all the Build Content Task / Content Feedback Work Items that need to be reviewed to the Splunk Working Group DLs, <usdeloittesocsplunkworkinggroup@deloitte.com>, in addition to setting "Requires SOC review for Volume Testing push" to true on the content feedback item
5. Tier 3 / Splunk Working Group Member provides preliminary feedback to be implemented before content is pushed to Volume Testing, or none if the content already meets expectations
6. Content team implements feedback
7. Content is ready for Volume Testing after updates are verified by Content Testing and Validation Team member
8. If there are major logic adjustments to the search query logic, the content team will move the Build Content Task back to WIP
9. Build content state should equal “SOC Review”



**##Ready for Volume Testing Board**
1. Build content work items should only be on this board after they have been reviewed by the SOC stakeholders, and any applicable feedback implemented to the query logic
1. Build content work items need to be on this board in order to run project s’ automation solution to create the stanza for savedsearches.conf in the DA-ESS-Americas-DevContent Splunk app
1. Project S will create a pull request for each content’s back-end stanza to be merged into the savedsearches.conf file in the DA-ESS-Americas-DevContent Splunk app
1. Notable events should have “DEV” in the title 
1. SecOps adaptive response action bit should equal 0 at this stage
1. All content is pushed into splunk with disabled = 1 at this stage
1. Build content state should equal “Volume Testing”


**##Volume Testing Board - CTVT, Volume Testing Board - Alert Maturity and Volume Testing Board - GPS**
1. For build content work items to be on this board, they must be enabled and scheduled to run and produce notable events in Splunk
1. The Splunk working group from the SOC has 5 business days to review and comment on the volume of notable events produced and any other related feedback
1. The project S development team will implement suggested feedback within reason and document all changes to a content item in the linked content feedback work item
1. Any related discussion between the Splunk working group and project s development team should be documented in the discussion portion of the content feedback work item
1. If no feedback is documented on the content feedback work item 5 business days after its initial push to volume testing, project S will follow up with the splunk working group to ensure there is no feedback and this particular content item can be pushed to production for active monitoring
1. Build content state should equal “Volume Testing” 
##Ready for Production Board
1. Build content work items should be moved to this board if and only if they have received explicit sign off to be moved to production in the form of a content feedback work item
1. If signoff has been received, project S will create a pull request to push the content into production
1. While in the "Ready for Production" column, content must be tagged with one of the following:
   - "SNOW"
     - Content will produce ServiceNow tickets in production
   - "Dashboard"
     - Content will power a dashboard in production
   - "Report"
     - Content will produce a schedule report in production
1. Project S will remove “DEV” from all applicable places in the back end stanza
1. Project S will change the SecOps adaptive response action create security event bit from 0 to 1
1. Project S will create a pull request that:
-will remove the content’s stanza from the DevContent App
-Move the stanza to the matching FC app
-In the pull request, project S will link the work items they are pushing to production
-When pull request policies succeed, project S will ensure that the checkbox for completing work items is left unchecked 
-This is due to the process of pushing content disabled and project s needing to manually enable each content item 
1. Build content state equals “Ready for Production”



**##	Enabled In Production**
1. Build content items live on this board if they are enabled and scheduled to run in Splunk production
1. Build content state should equal closed


##	On Hold Column
- Any reason why a content item is on hold must be clearly documented in the linked content feedback work item
- Reasons why build content could be “on-hold” and live on this board:

-Build content work items live on this column if and only if a consensus was not reached between the SOC stakeholders and project s development team with respect to monitoring logic
-Filtering out results from volume of data returned
-Awaiting approvals from data source owners to filter out specific results
-Any other related reasons why the SOC does not want to consume the alerts project S develops
- State should equal “On Hold” for this board
