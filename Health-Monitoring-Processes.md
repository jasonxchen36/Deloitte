Splunk Monitoring

Types of monitoring:

1. Data Monitoring Search
  - **No data in index or significant drop in ingest volume**
    - An alert from the Distributed Monitoring Console (DMC) is triggered due to an index that is not receiving data for over 24 hours or due to a significant drop in data ingest volume
    - Work Item (WI) is automatically created by Azure Logic and added to Run team boards
      - WI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
    - Email is automatically sent to stakeholder distribution list with WI details and link to WI
    - Run leads assign WI work item to available Run Engineer
      - Run lead is responsible for managing Run Engineer work load to make sure resolution can be met within SLA
    - Run Engineer starts resolution process by following alert-specific playbook
    - **No Data in Index Playbook**
      - Run Engineer accesses Splunk GUI and verifies the accuracy of the alert
      - Verify that no data is present in the index for the past 24 hours from the time the alert was triggered
        - If data is in index over past 24 hours, this could imply that data has since started to return to the index
          - Verify data volume for past 24 hours vs a daily average timechart over the past 30 days
          - If data volume is significantly lower, reclassify WI as a volume reduction in index and work the WI with the Significant Drop in Data Ingest Volume Playbook
      - If alert is  **not ** verified, initiate the False Positive process
      - If alert is verified and there is no data in the index, gather initial troubleshooting data
        - Navigate to the index dashboard and determine data source ingest type (e.g., API) and source of data ingest (e.g., hostname of Heavy Forwarder)
        - Estimate ingest rates and intervals by reviewing Splunk search charts and using built in visualizations
          - For ingest methods such as API and DB pulls, ingest intervals are usually set in the Heavy Forwarder configuration files
        - Estimate the time that the data stopped feeding to Splunk using search and ingest interval estimates in the previous step
        - Leverage Splunk internal logs to determine if any errors are present that are related to the data source in question – use variations of the data source name, app name, hostname related to ingest, etc. to investigate
        - Review past WIs to determine if past issues have been experienced with data source
          - If issue is similar to past issue, verify that same symptoms are present and attempt resolution by following steps taken in past WI
        - Document initial troubleshooting data on the WI
          **This is an important step for handing off any unfinished work to the next shift**
      - Troubleshooting steps
        - If an obvious error was found in initial troubleshooting data gathering, proceed to work the error until a resolution is found – leverage Engineering resources including original Engineering data source onboard resource for any assistance
        - Verify host that is responsible for ingest is operational
          - Check host SSH access
            - Verify Splunk daemon is running
          - If applicable, check Splunk GUI access
        - Verify ingest inputs are enabled
        - For syslog ingest, verify rsyslog configurations such as network port actively listening and syslog mount storage capacity
        - For API and DB ingest, verify network connectivity to data source endpoints using telnet and network port number
        - For ingests requiring credentials, use Splunk internal logs to verify that credentials are still valid
        - Determine if any Devops Work Items or Pull Requests have been worked on in past 48 hours that are related to the data source
          - If a Devops Work Item or Pull Request is found, review work performed and determine if it could potentially be the cause of missing data
            - If unsure, leverage other Engineering resources – including Engineer that last worked on data source in question
        - Work with Data Center team to determine if any networking, storage, or OS issue alerts are affecting Splunk which could potentially have an impact on ingest (e.g., intermittent networking causing packet loss)
        - If above troubleshooting steps have not led to a resolution, work with Run leads to contact the data source owners to determine if any changes have been made by data source team or if the data source team is currently experiencing any issues with the data source
          - If issue is found to be on data source side, work towards resolution with data source team and determine timelines for any resolutions performed by data source owners
          - Update Run leads and stakeholders by emailing resolution timeline from data source team
          - Work with data source owner to determine notification mechanism for reporting any future issues to Engineering
        - \*\*If no root cause can be determined by above troubleshooting steps, work with Run leads to open a Splunk Support ticket
          - Attempt to get on a call with Splunk Support Engineer and troubleshoot issue
            - If a call is not possible right away, work via email until a call can be scheduled and performed
          - Update WI with all Splunk Support suggestions and any communications over email
            - Make sure to include Splunk Support ticket number and any other relevant data in the WI in case Support case needs to be handed to next shift
        - Document all troubleshooting steps on the WI
          - \*This is an important step for handing off any unfinished work to the next shift
      - Resolution
        - Once root cause is identified, work with necessary resources to resolve root cause issue
        - Once resolution is achieved, verify that data is back in index and volume of data is consistent with daily average over past 30 days
        - Send email notification to stakeholders that data is back in index
        - Open Recovery Work Item (RWI) and link to WI as a Related Work Item
        - Set state of WI to Resolved and work with Run leads to complete Recovery process
    - **Significant Drop in Data Ingest Volume Playbook**
      - Run Engineer accesses Splunk GUI and verifies the accuracy of the alert
      - Use Splunk search charts and/or timechart command to verify count of events in past 24 hours is significantly lower than daily average over past 30 days
      - If alert is  **not ** verified, initiate the False Positive process
      - If alert is verified and there is a significant drop in data ingest volume, gather initial troubleshooting data
        - For single inputs that bring in multiple data sources (e.g., Office 365, Azure Active Directory), determine if the significant drop in data ingest volume is due to data missing from a specific sourcetype, Workload, etc.
          - g., Azure Active Directory decrease in ingest volume could be due to Sign In sourcetype missing while Audit sourcetype is still ingesting data
          - g., Office 365 decrease in ingest volume could be due to Exchange and SharePoint Workloads missing while the rest of the Workloads are still ingesting data
          - \*\ ***Important note** : Review alert logic to determine if single input data source has multiple types of data its tracking such as the two examples above, this can potentially save a lot of troubleshooting time
        - Navigate to the index dashboard and determine data source ingest type (e.g., API) and source of data ingest (e.g., hostname of Heavy Forwarder)
        - Estimate ingest rates and intervals by reviewing Splunk search charts and using built in visualizations
          - For ingest methods such as API and DB pulls, ingest intervals are usually set in the Heavy Forwarder configuration files
        - Estimate the time that the data ingest volume drop occurred using search and ingest interval estimates in the previous step
        - Leverage Splunk internal logs to determine if any errors are present that are related to the data source in question – use variations of the data source name, app name, hostname related to ingest, etc. to investigate
        - Review past WIs to determine if past issues have been experienced with data source
          - If issue is similar to past issue, verify that same symptoms are present and attempt resolution by following steps taken in past WI
        - Document initial troubleshooting data on the WI
          - \*This is an important step for handing off any unfinished work to the next shift
      - Troubleshooting steps
        - If an obvious error was found in initial troubleshooting data gathering, proceed to work the error until a resolution is found – leverage Engineering resources including original Engineering data source onboard resource for any assistance
        - Determine if any Devops Work Items or Pull Requests have been worked on in past 48 hours that are related to the data source
          - If a Devops Work Item or Pull Request is found, review work performed and determine if it could potentially be the cause of missing data
            - If unsure, leverage other Engineering resources – including Engineer that last worked on data source in question
        - Work with Data Center team to determine if any networking, storage, or OS issue alerts are affecting Splunk which could potentially have an impact on ingest (e.g., intermittent networking causing packet loss)
        - If above troubleshooting steps have not led to a resolution, work with Run leads to contact the data source owners to determine if any changes have been made by data source team or if the data source team is currently experiencing any issues with the data source
          - If issue is found to be on data source side, work towards resolution with data source team and determine timelines for any resolutions performed by data source owners
          - Update Run leads and stakeholders by emailing resolution timeline from data source team
          - Work with data source owner to determine notification mechanism for reporting any future issues to Engineering
        - \*\*If no root cause can be determined by above troubleshooting steps, work with Run leads to open a Splunk Support ticket
          - Attempt to get on a call with Splunk Support Engineer and troubleshoot issue
            - If a call is not possible right away, work via email until a call can be scheduled and performed
          - Update WI with all Splunk Support suggestions and any communications over email
            - Make sure to include Splunk Support ticket number and any other relevant data in the WI in case Support case needs to be handed to next shift
        - Document all troubleshooting steps on the WI
          - \*This is an important step for handing off any unfinished work to the next shift
      - Resolution
        - Once root cause is identified, work with necessary resources to resolve root cause issue
        - Once resolution is achieved, verify that volume of data is consistent with daily average over past 30 days
        - Send email notification to stakeholders that data is back in index
        - Open Recovery Work Item (RWI) and link to WI as a Related Work Item
        - Set state of WI to Resolved and work with Run leads to complete Recovery process
  - **No data from hosts**
    - An alert from the Distributed Monitoring Console (DMC) is triggered due to hosts that have stopped sending data
    - Work Item (WI) is automatically created by Azure Logic and added to Run team boards
      - WI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
    - Email is automatically sent to stakeholder distribution list with WI details and link to WI  **only if the hosts are on a pre-determined list of hosts**
      - Potential reasons for additions to the pre-determined list are leadership requests, critical hosts such as domain controllers, special requests from stakeholders, etc.
    - Run leads assign WI work item to available Run Engineer
      - Run lead is responsible for managing Run Engineer work load to make sure resolution can be met within SLA
    - Run Engineer starts resolution process by following alert-specific playbook
    - **No Data From Host Playbook**
      - Run Engineer accesses Splunk GUI and verifies the accuracy of the alert
      - Use Splunk search charts and/or timechart command to verify host is not sending data to index within the past 24 hours
      - If alert is  **not ** verified, initiate the False Positive process
      - If alert is verified and there is no data in the index from the host in the past 24 hours, navigate to Deployment Server
        - Check Deployment Server to determine if host is actively phoning home
          - Check to make sure that correct Server Class and Apps are pushed to the Universal Forwarder
        - Navigate to CMDB and determine owner of host
        - Work with Run leads to contact owner of host
        - Work with owner of host to troubleshoot Splunk Universal Forwarder
          - Check if Splunk Daemon is running
          - Check connection to Deployment Server and verify that /opt/splunk/etc/apps/ has the same apps that are referenced in the Deployment Server
          - Check if networking is in place using telnet and network port
          - Check inputs.conf and outputs.conf to determine if any misconfigurations
          - Check SSL configurations
        - If root cause can&#39;t be determined by performing steps above, start to leverage troubleshooting steps from No Data in Index Playbook
          - Leverage Run and Build Engineering resources to determine if any other resources have ran into similar issues
        - \*\*If no root cause can be determined by above troubleshooting steps, work with Run leads to open a Splunk Support ticket
          - Attempt to get on a call with Splunk Support Engineer and troubleshoot issue
            - If a call is not possible right away, work via email until a call can be scheduled and performed
          - Update WI with all Splunk Support suggestions and any communications over email
            - Make sure to include Splunk Support ticket number and any other relevant data in the WI in case Support case needs to be handed to next shift
        - Document all troubleshooting steps on the WI
          - \*This is an important step for handing off any unfinished work to the next shift
      - Resolution
        - Once root cause is identified, work with necessary resources to resolve root cause issue
          - If root cause was determined to be fault of change or issue by owner of host, work
        - Once resolution is achieved, verify that volume of data is consistent with daily average over past 30 days
        - Send email notification to stakeholders that data is back in index (**only if initial WI required a stakeholder notification based on pre-determined list)**
        - Open Recovery Work Item (RWI) and link to WI as a Related Work Item
        - Set state of WI to Resolved and work with Run leads to complete Recovery process
2. Performance Monitoring Search
  - **Search performance**
    - An alert from the Distributed Monitoring Console (DMC) is triggered
    - Work Item (WI) is automatically created by Azure Logic and added to Run team boards
      - WI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
    - Email notification is not needed to stakeholders
    - Run leads assign WI work item to available Run Engineer
      - Run lead is responsible for managing Run Engineer work load to make sure resolution can be met within SLA
    - Run Engineer starts resolution process by following alert-specific playbook
    - **Generic Search Performance Monitoring Playbook**
      - Run Engineer accesses Splunk GUI and verifies the accuracy of the alert
      - If alert is  **not ** verified, initiate the False Positive process
      - If alert is verified, determine who Offender is and send email notification including initial alert generated by Splunk
        - If Offender is a Splunk app (some alerts only have app name, user name isn&#39;t present), leverage Engineering resources to determine who deployed the app and who owns the app
      - Email notification to Offender should include the following:
        - Forward the Splunk alert or attach the original alert to the email notification
        - Introduction of Engineer
        - Reason for reaching out – explain why the alert fired and that there is a performance issue when configured as such
        - Inform Offender that performance issue will need to be remediated
        - Offer assistance for remediation but leave the onus on the stakeholder for remediation
        - Provide timeline for expected remediation and inform Offender if not remediated within timeline that the knowledge object/configuration causing the performance issue will be disabled until fixed
      - Mark the time/date of initial communication with Offender in WI
      - Keep WI updated with status of communications with Offender
      - If timeline for expected remediation is reached without resolution from Offender, disable knowledge object/configuration
        - Send email notification to Offender that knowledge object/configuration has been disabled
        - Update WI state to Awaiting Resolution from Offender and mark date/time for SLA Close Date (the SLA was satisfied in this situation, don&#39;t close ticket in order to track Offender actions appropriately)
        - Continue to work with Offender until resolution is reached – however, onus should be on Offender to follow up and work with Engineer, Engineer is not responsible for follow up with Offender
      - If timeline for expected remediation is reached with a resolution from Offender, work with Offender to make changes in the next Change Window (if applicable)
        - If Offender is providing resolution, make sure to verify that the resolution meets Engineering standards and requirements
        - Verify resolution post Change Window with Offender
          - If resolution did not work or does not meet Engineering standards and requirements, the timeline for remediation does not change – the knowledge object/configuration should still be disabled at the end of the timeline
        - If resolution works and meets Engineering standards and requirements, close WI and mark date/time for SLA Close date
  - **Hardware performance (currently cloud based)**
    - **TBD**  – going to see what Jared comes up with for cloud and waiting to see what we can be receiving from the Data Center team
  - **Notable issues**  – (\*Note – Engineering is not responsible for issues with SNOW ticket creation, work with SNOW COE to determine any potential issues)
    - An alert from the Distributed Monitoring Console (DMC) is triggered
    - Work Item (WI) is automatically created by Azure Logic and added to Run team boards
      - WI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
    - Email notification to Engineering and GEMS leadership is sent with WI description and link to WI
    - Run leads assign WI work item to available Run Engineer
      - Run lead is responsible for managing Run Engineer work load to make sure resolution can be met within SLA
    - Run Engineer starts resolution process by following alert-specific playbook
    - **Generic Notable Issue Playbook**
      - Run Engineer accesses Splunk GUI and verifies the accuracy of the alert
      - If alert is  **not ** verified, initiate the False Positive process
      - If alert is verified, start troubleshooting the notable issue
        - Verify that production content items (mainly correlation searches labeled with FC-0\*) are Enabled
        - Verify in Splunk search that data is actively feeding into the index and/or data model that is being searched by the production content item
          - If data is not feeding in, work with Engineering resources to execute the No Data in Index Playbook
        - Verify Scheduled Times of production content items (mainly checking to see if Scheduled Times are in the past – this is a common issue)
        - Review Splunk internal Scheduler logs to determine if there is a high amount of Skipped, Continued, or Remote Errors for searches running in production content Splunk apps
        - Review content logic for any potential logic errors and execution/runtime errors
        - Review dispatch times and cron schedules of production content correlation searches
          - g., If a search is scheduled to run every 5 minutes but takes 10 minutes to run that will cause the search to not complete as expected
        - Verify that data model is working appropriately
        - Check data ingest latency against dispatch times and cron schedules
          - g., a search runs over the past 10 minutes, but data is ingested with a lag of 60 minutes
        - Review past WIs to determine if current symptoms match any past issues encountered
          - If issue is similar to past issue, verify that same symptoms are present and attempt resolution by following steps taken in past WI
        - \*\*If no root cause can be determined by above troubleshooting steps, work with Run leads to open a Splunk Support ticket
          - Attempt to get on a call with Splunk Support Engineer and troubleshoot issue
            - If a call is not possible right away, work via email until a call can be scheduled and performed
          - Update WI with all Splunk Support suggestions and any communications over email
            - Make sure to include Splunk Support ticket number and any other relevant data in the WI in case Support case needs to be handed to next shift
        - Document initial troubleshooting data on the WI
          - \*This is an important step for handing off any unfinished work to the next shift
      - Resolution
        - Once root cause is identified, work with necessary resources to resolve root cause issue
        - Once resolution is achieved, verify that notables have started firing again
        - Send email notification to Engineering and GEMS leadership that the notable issue has been resolved
        - Open Recovery Work Item (RWI) and link to WI as a Related Work Item
        - Set state of WI to Resolved and work with Run leads to complete Recovery process
3. Splunk Security Monitoring Search
  - **Splunk and Linux security alerts**
    - An alert from the Distributed Monitoring Console (DMC) is triggered
    - Security Monitoring Alert Work Item (SMAWI) is automatically created by Azure Logic and added to Run team boards
      - SMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
    - Email notification to Engineering (Build and Run) leadership is sent with SMAWI description and link to SMAWI
    - Run leads assign SMAWI to themselves, Run leadership, or Build leadership (dependent upon severity of SMAWI)
    - Lead starts resolution process by following alert-specific playbook
    - **Generic Splunk Driven Security Alert Playbook**
      - Lead accesses Splunk GUI and verifies the accuracy of the alert
      - If alert is  **not ** verified, initiate the False Positive process
      - If alert is verified, determine manager or lead of Offender
        - Check Offender list to determine if Offender is a repeat Offender
      - Based on severity level of the SMAWI, take the following enforcement action (these are generic enforcement actions, specific alerts may have different enforcement actions associated)
        - Low severity (1st Offense)
          - An email notification to the Offender and Offender&#39;s Manager and/or Lead with the original alert forwarded or attached
          - Lead may hand any explanations or retraining requested by Offender&#39;s Manager and/or Lead to Run Engineer
          - Offender is added to the Offender list
            - Include information on list such as Offender name, Offense type, Manager and/or Lead, Enforcement action taken, number of Offenses, etc.
          - Keep SMAWI updated with status of communications with Offender
          - Move SMAWI state to Resolved once all communications with Offender and Offender&#39;s Manager and/or Lead are complete
          - \*\*Repeat Offender (2nd and 3rd Offenses)
            - If Offender is on the Offender list, the following actions should take place
            - 2nd Offense
              - Lead works with Offender&#39;s Manager and/or Lead to enroll Offender in mandatory retraining
              - Lead records retraining start date and provides timeline for completion to Offender and Offender&#39;s Manager and/or Lead
              - Once Offender completes retraining, SMAWI is updated and closed
              - Update the Offender list with outcome of retraining and any other pertinent information
            - 3rd Offense
              - Lead informs Offender&#39;s Manager and/or Lead that a 3rd offense has been reached and the Offender&#39;s access to abused resource will be revoked
              - Lead immediately removes Offender&#39;s access to abused resource (e.g., removing SSH access)
              - Lead works with Engineering leadership, GEMS leadership (if applicable), and Offender&#39;s Manager and/or Lead to determine a path forward
              - Once a path forward is agreed upon, SMAWI is updated and state changed to Monitoring Extreme Offender (assuming that Offender&#39;s access is reinstated)
                - If Offender&#39;s access is not reinstated, change SMAWI state to Pending Leadership and wait for further direction
              - Offender is added to Extreme Offender list which will generate audit reports to Engineering leadership
              - Once Engineering leadership is satisfied with security posture of Offender, SMAWI state is moved to Resolved and Offender is removed from Extreme Offender list
                - \*Offender should stay on Offender list
            - 4th Offense and above
              - Immediately contact and assign SMAWI to Engineering leadership
        - Medium Severity (1st Offense)
          - An email notification to the Offender and Offender&#39;s Manager and/or Lead with the original alert forwarded or attached
          - Lead may hand any explanations or retraining requested by Offender&#39;s Manager and/or Lead to Run Engineer
          - Offender is added to the Offender list
            - Include information on list such as Offender name, Offense type, Manager and/or Lead, Enforcement action taken, number of Offenses, etc.
            - \*Number of Offenses on the Offender list for a Medium Severity alert is automatically set to 2
          - Keep SMAWI updated with status of communications with Offender
          - Move SMAWI state to Resolved once all communications with Offender and Offender&#39;s Manager and/or Lead are complete
          - \*\*Repeat Offender (2nd Offense)
            - If Offender is on the Offender list, the following actions should take place
            - 2nd Offense
              - Lead informs Offender&#39;s Manager and/or Lead that a 2nd offense has been reached and the Offender&#39;s access to abused resource will be revoked
              - Lead immediately removes Offender&#39;s access to abused resource (e.g., removing SSH access)
              - Lead works with Engineering leadership, GEMS leadership (if applicable), and Offender&#39;s Manager and/or Lead to determine a path forward
              - Once a path forward is agreed upon, SMAWI is updated and state changed to Monitoring Extreme Offender (assuming that Offender&#39;s access is reinstated)
                - If Offender&#39;s access is not reinstated, change SMAWI state to Pending Leadership and wait for further direction
              - Offender is added to Extreme Offender list which will generate audit reports to Engineering leadership
              - Once Engineering leadership is satisfied with security posture of Offender, SMAWI state is moved to Resolved and Offender is removed from Extreme Offender list
                - \*Offender should stay on Offender list
            - 3rd Offense and above
              - Immediately contact and assign SMAWI to Engineering leadership
        - High Severity (1st Offense)
          
            - Lead informs Offender&#39;s Manager and/or Lead that a high offense has been reached and the Offender&#39;s access to abused resource will be revoked
              - Go into the "Related Work" section of the associated work item, and add a new linked work item
                - Set link type to "Child"
                - Set work item to "Access"
                - Name the title "Revoke <offenders name here> access"
                - Make sure the area path is "Global FC Engineering Leads"
                - Assign work item to the lead who owns the AD group to which the offender belongs
                - Move Access Work Item to Access To Be Revoked board/state
            - Lead immediately removes Offender&#39;s access to abused resource (e.g., removing SSH access)
            - Offender is added to the Offender list
              - Include information on list such as Offender name, Offense type, Manager and/or Lead, Enforcement action taken, number of Offenses, etc.
              - \*Number of Offenses on the Offender list for a High Severity alert is automatically set to 3
            - Lead works with Engineering leadership, GEMS leadership (if applicable), and Offender&#39;s Manager and/or Lead to determine a path forward
            - Once a path forward is agreed upon, SMAWI is updated and state changed to Monitoring Extreme Offender (assuming that Offender&#39;s access is reinstated)
              - If Offender&#39;s access is not reinstated, leave SMAWI state in Pending Leadership and wait for further direction
            - Offender is added to Extreme Offender list which will generate audit reports to Engineering leadership
            - Once Engineering leadership is satisfied with security posture of Offender, SMAWI state is moved to Resolved and Offender is removed from Extreme Offender list
              - \*Offender should stay on Offender list

 Gap in monitoring recovery process (contingent on dashboard development):

- Run leads assign Run Engineer Recovery Work Item (RWI)
- Email notification is sent to Engineering and GEMS leadership with RWI description, start time, and link to RWI
- Engineer navigates to GAP Recovery Dashboard in Splunk Enterprise Security
- Engineer selects &quot;All Production Content&quot; or selects individual piece of production content
- Engineer enters date range to run production over
- Engineer runs the dashboard search
- Engineer verifies the notable results in the Notable Results panel of the GAP Recovery Dashboard
  - Verify that notables are creating Secops events, wait at least 1 hour for any Secops event creation lag (there could be as much as a 15 minute lag from notable to Secops event creation)
- Engineer updates RWI state to Ready for Secops Review
- Engineer assigns area path of RWI to Global FC Analysts
- Engineer assigns Global FC Analysts to the RWI and waits for comments from Global FC Analysts
- Global FC Analysts will review GAP Recovery Dashboard Notable Results panel and verify Engineer&#39;s findings
- Global FC Analysts will review Secops Incidents to determine if Secops Events are creating incidents
- Global FC Analysts will provide sign off date/time and flip the Verified boolean to True once verification of Recovery process is complete
- Engineer reassigns RWI to Engineering area path and changes state to Recovered
- Email notification is sent to Engineering and GEMS leadership that all Notables have been recovered

False Positives

There are two types of false positives:

- The person did what was reported, but had a good reason to do so
  - Move the work item to the resolve state
  - Since Splunk will automatically update, manually go into Splunk and delete the aforementioned offense for said offender
- The alert didn&#39;t work properly (logic wasn&#39;t working appropriately)
  - Alert requires additional tuning; engineer verifies findings with Global FC Engineering leads
  - Engineer updates WI or SMAWI state to False Positive
  - Since Splunk will automatically update, manually go into Splunk and delete the aforementioned offense for said offender
  - Engineer creates Tactical Content Work Item (TCWI) and links to WI or SMAWI and also links to the Splunk Security Monitoring Search Work Item (main work item associated with Alert)
  - Engineer works with other Global FC Engineers to tune the alert
  - Once tuned, Engineer updates TCWI state to Ready for Test and makes updates to the Splunk Security Monitoring Search Work Item
  - Engineer then updates alert logic and/or filters in DMC
  - Engineer verifies logic is firing appropriately
  - Once verified, Engineer updates TCWI state to Verified/Closed





4. Domain Controllers Monitoring

SCOPE 
To define the purpose of monitoring, remediating, and onboarding of Domain Controllers logs in Splunk. 

The AMER DMC at  https://usatramekj147.atrame.deloitte.com:8000 contains a dashboard titled “Tracking Domain Controllers (Deloitte)” in the “Meta Woot” app. This dashboard is powered by data sources like Kenna, meta woot and SNOW. 

Below are the key KPI(s) it displays, providing a high-level view of Domain Controllers in the environment.	
•	Active vs Inactive Domain Controllers
•	Active vs Inactive Domain Controllers by Member Firm 
•	List of Domain Controllers that have either stopped reporting to Splunk OR that exist in the environment but have never been onboarded into Splunk. 
•	A deep dive (Drill Down) per Domain Controller. 

Furthermore, the dashboard has the below filters to segregate Domain Controllers by:
•	Environment (Prod/Non-Prod/etc.)
•	Member Firm
•	FSS
•	Region 
•	Full Null Values
•	Threshold vs past 12-hour window. 

      -  Domain Controllers that have stopped reporting to Splunk

The AMER DMC will send a report with the list of Domain Controllers that stopped reporting to Splunk.
•	Reference the report “Tracking Domain Controllers Alert” fired every day at 8 am and 8 pm EST to get a list of domain controllers that have stopped reporting to Splunk as per their respective thresholds set. 
•	Identify if partial data sources/ event codes are coming in or whether ALL logs from domain controllers have ceased to come in.
•	If partial data sources/ event codes are missing, check to ensure the host has received all apps from its relevant deployment server and has phoned home.
•	If not phoned home, check splunk internal logs, OS logs, splunkd service status to deduce the problem.
•	If All logs have ceased to feed, check the last group of events and pinpoint a timeframe when it stopped reporting. 
•	Look for its internal logs and pinpoint timeframe when the host stopped reporting.
•	Look for errors or warnings in internal logs within the time range the host stopped reporting.
•	Based on the information gathered by the internal logs, deduce potential reasons and reach out to the domain controllers owner / member firm point of contact with steps for them to follow to remediate.
•	Create WI and set tagging to “Troubleshoot” in Azure Ops. 
•	If a SNOW ticket is requested, create one for the Team who owns the Domain Controllers.
•	Once the appropriate changes are made upon approvals, validate the issue has been resolved by checking latest logs of the domain controller.
•	Validate the domain controller is reporting by cross referencing it in the aforementioned domain controller meta woot dashboard. 
•	Look out for the next report and ensure the same domain controller is not in the next remediation list.
•	If it is, proceed with a deeper RCA to ensure issues ceases to persist.

     -  Domain Controllers that are in the environment but not on-boarded to Splunk ( net-new)

•	Identify the Domain Controllers that have the field value “Not Reported in Splunk” from the dashboard. 
•	Confirm the environment to which the Domain Controllers need to be onboarded.
•	Create a WI in Azure Ops and tag “Onboarding”
•	Generate a weekly list and confirm with the MF if these are net-new domain controllers. 
•	If net-new, initiate the onboarding process by ensuring they are phoning home to the relevant Deployment Server and receiving the relevant apps
•	If not reporting to Deployment Server, initiate the conversation with MF POC to get all the pre-requisites (port enablement, firewall rules, UF installation, deploymentclient.conf; etc.) completed. 
•	Initiate a change request to onboard the Domain Controllers. 
•	Validate the change has been successful and the Domain Controllers are no longer in the “not-reporting Domain Controllers” report.

     -  Exception Process 

•       In case there are client or regulatory reasons, a Member Firm may elect not to onboard the domain controller. In such a case the Member Firm needs to follow the Exception Process outlined below.
•	Initiate an email thread and guide the MF POC with the following exception procedure.
•	Request the MF POC to address the below form. The form can also be found in SNOW. Link here: https://deloitteglobal.service-now.com/sp?id=sc_cat_item&sys_id=84c6c452e7600300dd926217c2f6a980

Deloitte Global — Cybersecurity Exceptions Local Approval Form
Please complete all questions and send this Cybersecurity Exception Local Approval Form (this “Form”) to the Deloitte Global Cybersecurity Exceptions Management Team (“DTTL Cyber Exceptions”) for review. Please be as clear and detailed as possible in each response. Please note that the exception will need to be approved by the Global authorizing entity or delegates (i.e., Global Chief Information Security Officer and Global Chief Risk Officer). You will be contacted by someone from DTTL Cyber Exceptions following completion and submission of this Form.

GLOBAL CYBERSECURITY EXCEPTION INFORMATION
Date of Request: 	
Requesting Person (Person filling out Form): 	
Requesting Member Firm:  	
Member Firm Reputation and Risk Leader:  	
Member Firm Chief Information Officer or delegate (i.e., Chief Information Security Officer)	
Start date of the exception:	
End date of the exception:  	
Global PM40 Cybersecurity Policy and/or Standard requirement for which an exception is being requested:	
Rationale for exception:
•	Description of the rationale for the exception detailing relevant background for why this exception is required. 
•	Detail any information related to business and/or client requirements, technical limitations, cost restrictions that necessitate this exception to be granted.	

Risk Description:
•	Description of the potential impact on the Deloitte brand, financial impact, potential for a systemic breach with details of the risk and vulnerabilities, potential for a regulatory breach and likely impact, as well as the potential for any disruption to the continuity of Deloitte operations.
	
Compensating Controls:
•	Describe the compensating controls that will be / have already been put in place to mitigate the risks that will apply as a result of this exception request being granted. 
•	Please describe how these controls will mitigate the resultant risk.
	
Action Plan:
•	Detailed plan outlining actions needed to reach one or more goals to reach compliancy. 	
Classification and description of the data impacted
•	High-risk confidential, confidential, or public
•	Provide relevant background information on the type of data impacted by the risk. 
o	This should include details of PII, confidential client information, Deloitte intellectual property (IP) that may be exposed as a result on this exception.
	


AFFIRMATION
Affirmation- ACTION REQUIRED
Confirmation Required of Member Firm Requesting a Cybersecurity Exception

Deviations to Global PM40 Policies and Standards have the potential to create significant risk for Deloitte. Exceptions to Global PM40 Polices and Standards should be reviewed and endorsed by the local authorizing entity (i.e., typically where the exception originates), and then submitted to the Deloitte Global authorizing entity for review and approval.  The requesting entity (i.e., member firm) is responsible for tracking the progress of and implementing action plans agreed to as part of the exception request. 

The undersigned member firm Reputation and Risk Leader and Member Firm Chief Information Officer or delegate (i.e., Chief Information Security Officer) confirms the following:

1.	I have read the exceptions request details above and verify that the information contained is accurate to the best of my knowledge. 
2.	I am explicitly acknowledging/accepting the risks (risks to my member firm and the Deloitte organization generally) arising from such exception.
3.	I will keep Deloitte Global informed of any changes in circumstances or updates applicable to this exception request.



_____________________________________________
Signature of Member Firm Reputation and Risk Leader

_____________________________________________
Signature of Member Firm Chief Information Officer or delegate (i.e., Chief Information Security Officer)

Deloitte refers to one or more of Deloitte Touche Tohmatsu Limited (“DTTL”), its global network of member firms, and their related entities (collectively, the “Deloitte organization”). DTTL (also referred to as “Deloitte Global”) and each of its member firms and related entities are legally separate and independent entities, which cannot obligate or bind each other in respect of third parties. DTTL and each DTTL member firm and related entity is liable only for its own acts and omissions, and not those of each other. DTTL does not provide services to clients. Please see www.deloitte.com/about to learn more.

This publication and any attachment to it is for internal distribution among personnel of the Deloitte organization. It may contain confidential information and is intended solely for the use of the individual or entity to whom it is addressed. If you are not the intended recipient, please notify us immediately and then please delete this publication and all copies of it on your system. Please do not use this publication in any way.

None of DTTL, its member firms, related entities, employees or agents shall be responsible for any loss or damage whatsoever arising directly or indirectly in connection with any person relying on this publication. DTTL and each of its member firms, and their related entities, are legally separate and independent entities.

Copyright © 2021 For information, contact Deloitte Global.

