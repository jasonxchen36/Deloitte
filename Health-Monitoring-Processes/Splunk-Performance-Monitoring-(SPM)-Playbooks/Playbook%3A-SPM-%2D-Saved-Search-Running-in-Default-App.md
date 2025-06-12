**[Alert is Decommissioned]()**

# **Playbook: SPM - Saved Search Running in Default App**

An alert from the Distributed Monitoring Console (DMC) is triggered due to a search/report or Data model acceleration is running on non-approved application on Splunk. 

Health Monitoring Alert Work Item (HMAWI) is automatically created by Azure Logic and added to Health Monitoring Board &quot;New&quot; column.

HMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution.

HM team will assign HMAWI work item to available team member.

HM team is responsible for managing HM team member workload to make sure resolution can be met within SLA.

HM team member starts resolution process by following alert-specific playbook

**Playbook: SPM - Saved Search Running in Default App**

1. SPM - Saved Search Running in Default App:
2. HM team member moves HMAWI to &quot;verification of alert&quot; column on Health Monitoring team boards.
3.HM team member accesses Splunk GUI and verifies the search/report Data model name by running the same search provided below:

```
   index=\_internal sourcetype=scheduler
   | search
      [| inputlookup app\_user\_filter.csv
       | stats values(app) as app
       | table app]
   | search NOT
      [| inputlookup app\_user\_filter.csv
       | stats values(user) as user
       | table user]
 | stats count values(host) as host values(savedsearch\_name) as savedsearch\_name values(app) as app by user
 | fields user host savedsearch\_name app count
```
After performing the above steps

HM team member will move the HMAWI to &quot;investigating the alert&quot;.

And then HM team member will follow the steps provided below:

1. Check if the saved search is running in other than one of the DA-ESS-FC0XX (DA-ESS-FC0XX) apps.
 (DA-ESS-FC01 (DA-ESS-FC01) **TO** DA-ESS-FC035 (DA-ESS-FC035).


2. If the app seems to be one of them, then HM team member will move the HMAWI to &quot;false positive&quot; column on run team boards and inform the Deloitte SIEM Health Monitoring team to fine tune the alert.
3. If not, App name does not match with the Saved search name, Try contacting the content team to move the saved search to the right app.


4. Or if the saved search is having a different FC number than the App FC number, Try comparing the FC **Number** form the App name to the FC\*Number\* in the Saved search name. See if both are same. If that&#39;s the case, Inform the content team to move the saved search to the right app.

1. After completing Troubleshooting and resolving the problem, Then HM team member will move the HMAWI to &quot;solution implemented&quot; and inform the stake holder/creator of the report through email cc&#39;ed Deloitte SIEM Health Monitoring DL &quot;**deloittesiemhealthmonitoringteam@deloitte.com**&quot;.


Additional Troubleshooting steps:

1. While performing the above troubleshooting steps if HM team member faces any restriction like permission related issue for enabling disabling acceleration reach out to the SIEM Engineering team for additional troubleshooting support.

If SIEM Engineering teams is unable to find root cause, then open Splunk Support case for further troubleshooting

1. HM team member updates root cause identified, solution identified, solution implemented fields on HMAWIs.
2. HM team member moves HMAWI to closed column &amp; state.
3. HM team member notifies Health Monitoring team that issue has been resolved.