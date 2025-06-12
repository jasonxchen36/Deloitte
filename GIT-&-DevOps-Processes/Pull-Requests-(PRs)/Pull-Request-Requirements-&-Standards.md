#**WORK IN PROGRESS**

## Change Window Times and Submission Deadlines
- All times are in ***Eastern Time Zone (ET)***
- ***Minor*** changes typically consist of less than 10 modified lines within an existing app/app version
- ***Intermediate*** changes typically consist of more than 10 modified lines within an existing app/app version
- ***Major*** changes are new apps/app versions
- If there are concerns about a deadline/requirement, changes should be submitted as early as possible
- All updates/corrections to pull requests must be completed by 12P on the day before the change
   - i.e For the "*Prod* Th @ 9P-12A" change window, updates/corrections to the pull request must be completed by Wed @ 12P
   - The purpose of the submission deadlines are to provide enough time for both reviewers and requestors to meet the update/correction deadline

Change<br>Window | | Submission<br>Deadlines | | Change<br>Deadline|
|:--:|:--:|:--:|:--:|:--:|
 **Day/Time** | **Minor** | **Intermediate** | **Major** | **Day/Time** |
| *AMER Stage* Mon @ 11A-12P | Fri @ 12P | Fri @ 12P | Fri @ 12P | Mon @ 9A|
| *AMER Stage* Wed @ 11A-12P | Tu @ 12P | Tu @ 12P | Tu @ 12P | Wed @ 9A |
| *AMER Stage* Fri @ 11A-12P | Th @ 12P | Th @ 12P | Th @ 12P | Fri @ 9A |
| *AMER Prod* Mon @ 11:55P-2:55A | Fri @ 1A | Th @ 12P | Tu @ 12P | Fri @ 12P |
| *AMER Prod* Th @ 11:55P-2:55A | Wed @ 1A | Tu @ 12P | Fri @ 12P | Wed @ 12P |
| *EMEA Stage* Mon @ 12P-2P |  |  |  |  |
| *EMEA Stage* Wed @ 12P-2P |  |  |  |  |
| *EMEA Stage* Fri @ 12P-2P |  |  |  |  |
| *EMEA Prod* Mon @ 3P-6P |  |  |  |  |
| *EMEA Prod* Th @ 3P-6P|  |  |  |  |
| *APAC Stage* Mon @5A-6A |  |  |  |  |
| *APAC Stage* Wed @5A-6A |  |  |  |  |
| *APAC Stage* Fri @5A-6A |  |  |  |  |
| *APAC Prod* Mon @ 11A-2P |  |  |  |  |
| *APAC Prod* Th @ 11A-2P |  |  |  |  |

## PR Standards
- All searches must have a run time of less than 2 minutes unless an exception is received
- All PRs for Splunk permission files are reviewed by the Permissions Monitoring team
- Apps going to SHC and IC can not have a bin directory unless an exception is received
- Searches can not be scheduled (no cron) unless an exception is received
   - If an exception is received, logic, dispatch, and cron must be reviewed by Global FC Engineering
- If a search is not scheduled and used for a dashboard, it must be configured in the dashboard XML and not as a separate saved search
- Scheduled searches are not allowed to have acceleration enabled (auto-summarization = 0)
- Real time searches are not allowed
- All searches must be pushed from Devops with disabled = 1 in each stanza, they will then be enabled in the GUI the following day
- Lookup files are not allowed to be pushed via Devops (logic and lookup definitions for dynamic lookups can be pushed)
- Edits to data model constraints are not allowed to be pushed via DevOps. They must be done via the GUI with the right access. 
- Permissions files (metadata folder) in apps have to follow one of the [known default.meta files](/GIT-&-DevOps-Processes/Known-default.meta-Files) unless an exception is received/approved
- All Pull Requests (PRs) will be abandoned if they are over 2 weeks old
- All PR's must have a production purpose and approved audience. Configurations that will not be used will be rejected from going to production. For example:
   - CIM validation for security content or SOC request
   - Dashboards must be utilized by an agreed upon audience
- Limit commits to 1 time per pull request

## PR Requesters Best Practices
- Wait for pipeline execution to finish and review pipeline messages before you ask Approvers to review the PR.
Requester, those error messages are mainly for you! :)
- Fix detected issues if possible, otherwise, add a comment with the reason why any error message should be bypassed.

  *Example: In you are making any change not tested in staging you have to fix it by pushing change to Staging and test it or add the reason why change was not tested in Staging before go to Production.*

  Think that the more information the approvers have, the more fluid the approval process will be.

- Join Change Review scheduled calls, especially if you have doubts about pipeline messages or you need any kind of assistance from Architecture Team managing apps or using DevOps.

**Note:** *Cloud Validation* pipeline errors in **AMER** for **NOT SYNCHED APPS** can be ignored by now.

## PR Approvers Best Practices
- Review PR periodically not only "on-demand". Maybe daily could be a good habit. 
  
- Work in advance: avoid to complete many PRs near to Change Window otherwise pipeline becomes bottleneck.

- Do not approve PRs if the pipeline is queued or running.

- Join Change Review scheduled calls.

**Note:** *Cloud Validation* pipeline errors in **AMER** for **NOT SYNCHED APPS*** can be ignored by now.

## Future Enhancements
- Poor quality PR tracking and remediation 
   - Tracking users that repeatedly submit poor quality pull requests, remediation may involve removal of privileges to submit PRs until training has been completed
- SHC and Cloud Validation build pipelines will be merged into on.
- Pipeline checks will be revisited to fit new Splunk Cloud environment.

----

#AMER, EMEA, APAC Splunk Production and Staging Change schedule

**The Global Fusion Center Engineering team will be making changes to AMER/EMEA/APAC Splunk Production and Staging environment as per the following schedule**

===================================================================================
| **Description** |     **Time**       |     
|---|---|
| AMER Splunk Production Environment                                                               |  Every Tuesday and Friday at 02:30 a.m EST | 
|AMER Splunk Staging Environment  | Every Monday, Wednesday and Friday at 6:30 a.m EST|
|AMER Splunk DEV Environment  | Every Monday, Tuesday, Wednesday, Thursday and Friday at 11:00 am EST|
| EMEA Splunk Production Environment                                                               |  Every Monday and Thursday at 3:00 p.m EST | 
|EMEA Splunk Staging Environment  | Every Monday, Wednesday and Friday at 2:00 pm EST|
|EMEA Splunk DEV Environment  | Every Monday, Tuesday, Wednesday, Thursday and Friday at 11:00 am EST|
| APAC Splunk Production Environment                                                               |  Every Monday and Thursday at 11:00 a.m EST | 
|APAC Splunk Staging Environment  | Every Monday, Wednesday and Friday at 5:00 am EST|
|APAC Splunk DEV Environment  | Every Monday, Tuesday, Wednesday, Thursday and Friday at 11:00 am EST|

===================================================================================
===================================================================================
===================================================================================
**Below are the details of the Team responsible for these changes**

| **Splunk Environments** |     **Team performing changes**       |     
|---|---|
| AMER Splunk Production/Staging Pushes   |  APAC GEMS Engineering | 
| EMEA Splunk Production/Staging Pushes   |  AMER GEMS Engineering | 
| APAC Splunk Production/Staging Pushes   |  EMEA GEMS Engineering | 