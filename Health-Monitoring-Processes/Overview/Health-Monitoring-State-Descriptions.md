This page describes the boards and states of the Global FC Splunk Monitoring Boards and how to move from one board to the next. 

#Global FC Monitoring Boards


##4 work item types used
- Performance Monitoring Search 
-- Monitors for various search performance issues or users using bad SPL practice
- Data Monitoring Search
-- Monitors for health of data in indexes or hosts
- Health Monitoring Search
-- Monitors for health of overall Splunk infrastructure
- Security Monitoring Search 
-- Monitors for various security events in the Splunk core environment

##Not Started
- Splunk Monitoring (SM) search has not been started and is waiting to be assigned to Engineer
- SM search is assigned to Engineer and WI board/state is moved to Logic WIP

##On Hold
- SM search is moved to On Hold if the search can't currently be tuned or if there is leadership discussion on fidelity of the search 
- On Hold reason should be documented in the description of the WI
- SM search is moved off of On Hold and to respective board/state when the above is resolved 

##Logic WIP
- Splunk Monitoring engineer onboards/gathers the data required for SM Search
- SM Engineer creates appropriate KnowledgeObjects/SPL required for SM Search
- Once initial SM search is developed, Engineering moves board/state to Tuning

##Tuning
- SM search is tuned by Engineer to ensure accuracy of the alert, high fidelity, and an appropriate volume for the Engineering team to respond to
- Engineering lead reviews tuned search and gives sign off that it is completed
- Once sign off from Engineering lead is received, WI board/state is moved to Logic Completed

##Deprecated
- Any SM search Work Item that was completed but is no longer required is moved to the deprecated state and the rationale for deprecation is added to the comments of the work item

##Logic Completed
- SM search logic is complete and fully documented on SM work item
- If alert is to be automated, Engineer verifies alert volume with a member from the Splunk Monitoring team, Splunk Monitoring Engineer will add necessary conditions to Azure Logic app
- Splunk Monitoring Engineer tests automation of the SM search and verifies automatic work item creation
- Splunk Monitoring Engineer uses playbook templates to create new playbook and assign to automation 
- Splunk Monitoring Engineer moves WI board/state to Complete -- Automated

##Completed - General
- This column intends to hold general health monitoring tasks that are completed

##Completed - Lookup Gen
- This column intends to hold lookup generator searches that are completed

##Completed - Report/Dashboard
- This column intends to hold report or dashboard work items that are completed

##Complete -- Email
- SM search logic is deployed to appropriate regional DMC and turned on
- This column intends to hold and monitoring alerts that need to be enabled but not automated

##Complete -- Automated
- Splunk Monitoring Engineer sends email to stakeholders to communicate that SM search is now live and automated
- SM search WI stays in Automated board/state until it needs to be tuned or it is deprecated

