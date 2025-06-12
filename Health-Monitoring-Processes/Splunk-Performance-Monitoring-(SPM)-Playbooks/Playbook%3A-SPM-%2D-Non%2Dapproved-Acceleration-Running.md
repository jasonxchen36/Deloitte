**[Alert is Decommission]()**

# **Playbook: SPM – Non-approved acceleration running** 

An alert from the Distributed Monitoring Console (DMC) is triggered due to an acceleration running in a non-approved app. This should be disabled at earliest convenience.

Search Performance Monitoring Alert Work Item (SPMAWI) is automatically created by Azure Logic and added to Health Monitoring Team board on the "New" column.

SPMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution.

HM Team will assign SPMAWI work item to available team member.

HM Team is responsible for managing Run Engineer workload to make sure resolution can be met within SLA.

HM Team will start resolution process by following alert-specific playbook.

**Playbook: SPM – Non-approved Acceleration Running**

SPM – Non-approved acceleration running:

1. HM team member moves SPMAWI to &quot;Active&quot; column on Health Monitoring Team board.
2. HM team member Splunk GUI and verifies the veracity of the triggered alert by running the following query and checking if results are the same as the received on the SPMAWI:


```
index=_internal sourcetype=scheduler search_type=datamodel_acceleration OR search_type=report_acceleration (app!=Splunk_SA_CIM AND app!=DA* AND app!=SA*)
| stats count values(host) as host values(savedsearch_name) as "Saved Search" values(user) as user values(search_type) as type by app
| fields app, host, user, type, "Saved Search"
```


When finished with above steps, HM team member will follow the steps provided below:

1. Check the app name.

![image.png](/.attachments/image-f17705fd-6c1e-4475-b433-608af2316bcc.png)

2. Check the host. If you see a host which is not a Search head but any others like Deployment server or a heavy forwarder, proceed to further steps to de-accelerate the search.

![image.png](/.attachments/image-2705119f-00c8-47aa-bce9-0c6e7f477b1a.png)
3. Check the name and type of the saved search that has been accelerated.

![image.png](/.attachments/image-f3725369-0484-4f07-b2e8-61cbba6fb6b1.png)

4. Check on each Search Head if acceleration has been enabled. If yes, this acceleration should be disabled with a Pull Request.
5. Search over Azure DevOps if there is a Work Item related with the Saved Search. If found, look in it for the stake holder/creator and contact him/her to further confirm if it was expected to be accelerated. Include this information as a comment on the SPMAWI.
6. If this is not an expected behavior, proceed to disable the acceleration and inform the stake holder/creator of the report through email cc&#39;ed Deloitte SIEM Health Monitoring DL **:** deloittesiemhealthmonitoringteam@deloitte.com Include this information as a comment on the SPMAWI.


7. Further investigate if this acceleration comes from some change made i.e. last push made or some duplicated alerts. This information should be included in the final report that will be sent to the stake holders/creator and include it as a comment on the SPMAWI.
8. After completing Troubleshooting and resolving the problem, Then HM team member will move the SPMAWI to &quot;Completed&quot; and inform the stake holder/creator with the evidence obtained on previous step through email cc&#39;ed Deloitte SIEM Health Monitoring DL: **deloittesiemhealthmonitoringteam@deloitte.com** 

Additional Troubleshooting steps:

1. While performing the above troubleshooting steps if HM team member faces any restriction like permission related issue for enabling disabling acceleration reach out to the SIEM Engineering team for additional troubleshooting support.

If SIEM Engineering teams is unable to find root cause, then open Splunk Support case for further troubleshooting

1. HM team member updates root cause identified, solution identified, solution implemented fields on SPMAWIs
2.  HM team member SPMAWI to closed column &amp; state
3.  HM team member notifies Health Monitoring Team that issue has been resolved.