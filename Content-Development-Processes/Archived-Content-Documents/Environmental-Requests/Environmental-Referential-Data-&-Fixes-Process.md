<b>Requesting environmental referential data</b> 
Scenario: Volume testing or production alert produces a false positive (determined after investigation) 
1.	Engineer or analyst creates an RFED (Request for Environmental Data) work item in DevOps for tracking purposes
•	RFED work item is linked to Build Content Task work item
2.	Work item is assigned to GEMS service owner & GEMS AMER lead
3.	GEMS service owner & GEMS AMER lead assign work item to designated analyst to find data
4.	Analyst completes the following steps:
•	Check SNOW and GLB to determine if data exists in one of the CMDBs
&ensp;&ensp;&ensp;&ensp;o	If so, reach out to the listed owner and determine if data is up to date – if not, work with owner to retrieve updated data using the following step
•	If data does not exist in the CMDB
&ensp;&ensp;&ensp;&ensp;o	Check contact list on DevOps wiki to determine who to reach out to
&ensp;&ensp;&ensp;&ensp;o	Send email to contact to gather data (if a new contact is not on the list, add to wiki list)
&ensp;&ensp;&ensp;&ensp;o	Add status and contact to RFED work item, follow up as needed
&ensp;&ensp;&ensp;&ensp;o	Once information is received, store in repository and contact CMDB team to update any out of date information (or add new data to CMDB)
&ensp;&ensp;&ensp;&ensp;o	Determine if the referential data is a one-time data ingest or if the data needs to be updated periodically (if so, work with owner and CMDB to determine method/mechanism)
&ensp;&ensp;&ensp;&ensp;o	Upload data to DA-ESS-Americas-Lookups app and document in the lookup tracker on SharePoint
5.	Analyst works with Engineering to determine best way to incorporate data into content logic
6.	Engineer adds new content logic incorporating data via DevOps pull request
7.	Once new content logic is pushed to production, analyst and engineer verify content logic is behaving appropriately
8.	Analyst and/or engineer close out RFED work item

<b>Fixing environmental issues</b>
Scenario: Environmental issue impacting the fidelity of alerts is identified 
1.	Engineer or Analyst creates EF (Environmental Fix) work item and links to Build Content Task work item
2.	Work item is assigned to GEMS service owner & GEMS AMER lead
3.	GEMS service owner & GEMS AMER lead assign work item to designated analyst to determine solution
4.	Analyst completes the following steps:
•	Check DevOps wiki contact list and start reaching out to asset owners
&ensp;&ensp;&ensp;&ensp;o	If contact information does not exist on the wiki, look on CMDB or reach out to GEMS service owner & GEMS AMER lead to escalate
•	Set up initial meeting with asset owner to describe potential security risks and issues that are coming from assets in question
&ensp;&ensp;&ensp;&ensp;o	In the future, we will determine a uniform approach to formalize our requests
&ensp;&ensp;&ensp;&ensp;o	Work with asset owner to determine fixes that are needed to fill security gaps
&ensp;&ensp;&ensp;&ensp;o	Track status on work item and update GEMS service owner, GEMS AMER lead and Engineering on a weekly touchpoint 
&ensp;&ensp;&ensp;&ensp;o	Once fix is implemented, verify with asset owner and through data in Splunk (and remove any temporary stop-gaps implemented while fix is in progress)
&ensp;&ensp;&ensp;&ensp;o	Document completion status on work item

<b>Reporting and tracking</b>
•	PMO to keep track of requests and makes sure they are being worked on
•	Report fixes made to leadership
•	Follow up on CMDB updates (reports to CMDB leadership)
•	Escalate roadblocks to leadership
