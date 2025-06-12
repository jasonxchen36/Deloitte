- An alert from the Distributed Monitoring Console (DMC) is triggered due to an index that is not receiving data for the specified threshold duration
- Data Monitoring Alert Work Item (DMAWI) is automatically created by Azure Logic and added to Health Monitoring boards on the &quot;New&quot; column
 - DMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
- HM team assign DMAWI work item to available Team member
- HM team is responsible for managing HM team member workload to make sure resolution can be met within SLA
- HM team member starts resolution process by following alert-specific playbook

**Playbook: DMC - No Data in Index** 


- HM team member moves DMAWI to &quot;verification of alert&quot; column on HM team boards
- HM team member accesses Splunk GUI and verifies the accuracy of the alert
- Verify that no data is present in the index for the specified threshold duration from the time the alert was triggered.
 - If data is in the index during the time the alert was triggered, this could imply that data has since started to return to the index
- If data has been restored by the time the HM team member performs the required alert verification
 - HM team member documents DMAWI with data showing restoration
  - HM team member moves DMAWI to the &quot;Data Restored&quot; column
- If alert is not verified, initiate the False Positive process
 - HM team member moves DMAWI to &quot;False Positive&quot; column on HM team boards

\*\*\* _Alert should only be moved to the &quot;False Positive&quot; column in the event the alert can be shown to be invalidly alerting. Identification of issue with alert is necessary for correction of &quot;False Positive&quot; alert._

- If alert is verified and there is no data in the index, gather initial troubleshooting data
  - HM team member moves DMAWI to &quot;Active&quot; column on HM team boards
  - Navigate to the Index Mapping dashboard on the ES SHC and determine data source ingest type (e.g., API) and source of data ingest (e.g., hostname of heavy forwarder)
  - Estimates ingest rates and intervals by reviewing Splunk search charts and using built in visualizations
    - For ingest methods such as API and DB pulls, ingest intervals are usually set in the heavy forwarder configuration files
  - Estimate the time that the data stopped feeding to Splunk using search and ingest interval estimates in the previous step
  - Leverage Splunk internal logs to determine if any errors are present that are related to the data source in question – use variations of the data source name, app name, hostname related to ingest, etc. to investigate
  - Review past DMAWIs to determine if past issues have been experienced with data source
    - If issue is similar to past issue, verify that same symptoms are present and attempt resolution by following steps taken in past DMAWI
  - Document initial troubleshooting data on the DMAWI

\*\*\* _This is an important step for handing off any unfinished work to the next shift as well as remediation of potential future alerts_

- **Troubleshooting steps**
  - If an obvious error was found in initial troubleshooting data gathering, proceed to work the error until a resolution is found – leverage Engineering resources including original Engineering data source onboard resource for any assistance
  - Verify host that is responsible for ingest is operational

      - Check host SSH access
        - Verify Splunk daemon is running
      - If applicable, check Splunk GUI access
  - Verify ingest inputs are enabled
  - For syslog ingest, verify rsyslog configurations such as network port actively listening and syslog mount storage capacity
  - For API and DB ingest, verify network connectivity to data source endpoints using telnet and network port number
  - For ingests requiring credentials, use Splunk internal logs to verify that credentials are still valid
  - Determine if any DevOps work items or pull requests have been worked on in past 48 hours that are related to the data source

      - If a DevOps Work Item or pull request is found, review work performed and determine if it could potentially be the cause of missing data
        - If unsure, leverage other Engineering resources – including Engineer that last worked on data source in question
  - Work with Data Center team to determine if any networking, storage, or OS issue alerts are affecting Splunk which could potentially have an impact on ingest (e.g., intermittent networking causing packet loss)
  - If above troubleshooting steps have not led to a resolution, work with HM leads to contact the data source owners to determine if any changes have been made by data source team or if the data source team is currently experiencing any issues with the data source

      - If issue is found to be on data source side, work towards resolution with data source team and determine timelines for any resolutions performed by data source owners
        - HM team member moves DMAWI to &quot;On Hold/Pending Stakeholder&quot; column on HM team boards
      - Update HM leads and stakeholders by emailing resolution timeline from data source team
      - Work with data source owner to determine notification mechanism for reporting any future issues to Engineering
  - \*\*\* If no root cause can be determined by above troubleshooting steps, work with HM team leads to open a Splunk Support ticket

      - Attempt to get on a call with Splunk support engineer and troubleshoot issue
        - If a call is not possible right away, work via email until a call can be scheduled and performed
      - Update DMAWI with all Splunk Support suggestions and any communications over email
        - Make sure to include Splunk Support ticket number and any other relevant data in the DMAWI in case Support case needs to be handed to next shift
  - Document all troubleshooting steps on the DMAWI

\*\*\* _This is an important step for handing off any unfinished work to the next shift as well as remediation of potential future alerts_

  - Resolution
  - Once root cause is identified, work with necessary resources to resolve root cause issue

      - HM team member moves DMAWI to &quot;Issue identified&quot; column on HM team boards
      - HM team member documents root cause on DMAWI
      - HM team member documents the solution to root cause on DMAWI
      - HM team member moves work item to &quot;Solution Identified&quot; column on HM team boards
      - Once resolution is achieved, verify that data is back in index and volume of data is consistent with daily average over past 30 days
        - HM team member moves DMAWI to &quot;Solution implemented&quot; column on HM team boards
        - After volume of data is verified to have returned to normal, HM team member moves DMAWI to &quot;SOC Notification&quot; column on HM team boards
      - After DMAWI is moved to &quot;SOC Notification&quot; column, and email is triggered to both the SOC and Engineer assigned to work item. This email tells the SOC to re-run content over the time period when data was missing from index
        - After SOC re-runs content, SOC is to coordinate with engineer assigned to ticket to let them know they can move the DMAWI to state = closed
      - Set state of DMAWI to completed