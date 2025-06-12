-  An alert from the Distributed Monitoring Console (DMC) is triggered
-  Security Monitoring Alert Work Item (SMAWI) is automatically created by Azure Logic App and added to Health Monitoring team boards 
-  SMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution
-  Email notification to Health Monitoring Team is sent with SMAWI description and link to SMAWI 
-  Health Monitoring team will assign SMAWI work item to themselves.
-  Lead starts resolution process by following alert-specific playbook
-  #**Playbook: SecMon – Clean Command on Splunk Backend**
   
   - P1 - High Severity - SLA 4 Hour Response
   - High Severity (1st Offense)
     - If the event is reviewed by the assigned lead and verified that the event occurred for legitimate reason, the user will be notified and there will be an &quot;exemption&quot; state assigned by the Health Monitoring Leads


     - Lead informs Offender&#39;s Manager and/or Lead that a high offense has been reached and the Offender&#39;s access to abused resource will be revoked
     - Lead immediately removes Offender&#39;s access to abused resource (e.g., removing SSH access)
     - Offender is added to the Offender list (Done automatically by Splunk)
       - Include information on list such as Offender name, Offense type, Manager and/or Lead, Enforcement action taken, number of Offenses, etc.
     - \*Number of Offenses on the Offender list for a High Severity alert is automatically set to 3 (Done automatically by Splunk)
     - Lead works with Health Monitoring leadership and Offender&#39;s Manager and/or Lead to determine a path forward
     - Once a path forward is agreed upon, SMAWI is updated and state changed to Monitoring Extreme Offender (assuming that Offender&#39;s access is reinstated)
       - If Offender&#39;s access is not reinstated, change SMAWI state to Pending Leadership and wait for further direction
     - Offender is added to Extreme Offender list which will generate audit reports to Health Monitoring leadership
     - Once Health Monitoring leadership is satisfied with security posture of Offender, SMAWI state is moved to Resolved and Offender is removed from Extreme Offender list
       - \*Offender should stay on Offender list