The following defines the Global FC Engineering Leads team board descriptions and their associated states: 

**New**

- Azure Logic creates a Security Monitoring Alert Work Item (SMAWI), which is automatically assigned to a lead and placed in the New board/state
- Global FC Engineering Lead assigns SMAWI to appropriate Engineering team lead based on severity of SMAWI
- Once Engineering team lead is assigned, Engineering team lead moves SMAWI board/state to Pending Investigation

**Pending Investigation** 

- Lead accesses Splunk GUI and verifies the accuracy of the alert
  - If alert is \*\*not \*\* verified, initiate the False Positive process and move to False Positive board/state
- If SMAWI is determined to be high severity, lead moves board/state to Pending Leadership
- Check Offender list to determine if offender is a repeat offender
  - If Offender is a repeat offender and has reached the highest number of offenses per that severity, move SMAWI board/state to Pending Leadership, and create Access Work Item (AWI) as per the alert playbook
  - For new or otherwise low-risk offenders, move board/state to Awaiting Resolution (AR) and follow the alert playbook for the appropriate severity

**Awaiting Resolution**

- Engineering Team Lead will follow the playbook
- Once work item is resolved, move board/state to Resolved

**Monitoring Extreme Offender**

- Extreme Offender list (extremeOffenderLookup) will generate audit reports (tbd) to Engineering leadership
- Once Engineering leadership is satisfied with security posture of Offender, SMAWI board/state is moved to Resolved and Offender is removed from Extreme Offender list

**Pending Leadership**

- Lead works with Engineering leadership, GEMS leadership (if applicable), and Offender&#39;s Manager and/or Lead to determine a path forward
- Once a path forward is agreed upon, SMAWI is updated and state changed to Monitoring Extreme Offender (assuming that Offender&#39;s access is reinstated)
  - If Offender&#39;s access is not reinstated, leave SMAWI state in Pending Leadership and wait for further direction

**Access To Be Revoked**

- Global FC Engineering lead who owns the respective AD group will review the Access Work Item and act as necessary
- Once a decision is reached, move Access Work Item board/state to Resolved

**False Positive**

- Refer to False Positive Playbook

**Resolved**

- SMAWI is resolved