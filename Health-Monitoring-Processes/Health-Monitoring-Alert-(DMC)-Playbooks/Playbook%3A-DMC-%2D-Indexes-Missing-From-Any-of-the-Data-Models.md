# **Playbook: Health Monitoring – Indexes missing from any of the Data Models**

An alert from the Search Head Cluster(SHC) is triggered due to an index that has left a Data Model which it belonged to. 

Search Performance Monitoring Alert Work Item (SPMAWI) is automatically created by Azure Logic and added to HM Team board on the &quot;New&quot; column. Also, an email is sent to **deloittesiemhealthmonitoringteam@deloitte.com**

SPMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution.

Health Monitoring team assign SPMAWI work item to available HM team member

Health Monitoring team is responsible for managing HM team member workload to make sure resolution can be met within SLA

HM team member starts resolution process by following alert-specific playbook

**Playbook: Health Monitoring – Indexes missing from any of the Data Models**

Health Monitoring – Indexes missing from any of the Data Models:

1. HM team member moves SPMAWI to &quot;Active&quot; column on HM Team board
2. HM team member accesses Splunk GUI and verifies the correct creation of the lookup on which this alert relies on. This lookup generation is scheduled to be done once a day.
3. HM team member accesses Splunk GUI and verifies the veracity of the triggered alert by running the following query and checking if results are the same as the received on the SPMAWI:

```
| datamodel 
| rex field=_raw "\"modelName\"\s*\:\s*\"(?<modelName>[^\"]+)\"" 
| fields modelName 
| table modelName 
| map maxsearches=40 search="tstats `summariesonly` count from datamodel=$modelName$ by sourcetype,index | eval dataModel=\"$modelName$\""
| fields- count
| lookup datamodelindex.csv dataModel index OUTPUT index as missing\_index
| inputlookup datamodelindex.csv append=true
| stats values(dataModel) as dataModel values(missing\_index) as missing\_index by index
| search NOT missing\_index=\*
```

When finished with above steps, HM team member will follow the steps provided below:

 ![](RackMultipart20200819-4-1w8czmg_html_b8ba0d1fb1972d5c.gif)
1. Check the index name:

![DMC1.png](/.attachments/DMC1-eaf1ac51-73d1-442e-8a4a-20091b1a5ea3.png)


2. Check that the field _indexcheck_ is empty. This field is used to control which indexes have left a data model and it should be empty if the alert has been triggered.
a.[](RackMultipart20200819-4-1w8czmg_html_386a04e9f253a3f9.gif) If alert is triggered and this field is not empty, reach out to [**deloittesiemhealthmonitoringteam@deloitte.com**](mailto:deloittesiemhealthmonitoringteam@deloitte.com) for this behavior to be checked.

 ![DMC 2.png](/.attachments/DMC%202-a6b91b43-9431-45e6-925d-488102006a13.png)
3. Search over Azure DevOps if there is a Work Item related with the index(es) gathered by the alert. If found, look in it for the stake holder/creator and contact him/her to further confirm if it was expected to be taken out from its data model. Include this information as a comment on the SPMAWI.

1. If this is not an expected behavior, confirm with the stakeholder if it should be re-included on the data model and start the procedure for it. Inform the stake holder/creator of the report of this situation through email cc&#39;ed Deloitte fusion DL: **deloittesiemhealthmonitoringteam@deloitte.com**. Include this information as a comment on the SPMAWI.

1. Further investigate if this removal comes from some change made i.e. last push made or some new feeds included. This information should be included in the final report that will be sent to the stake holders/creator and include it as a comment on the SPMAWI.

1. After completing Troubleshooting and resolving the problem, Then HM team member  will move the SPMAWI to &quot;Completed&quot; and inform the stake holder/creator with the evidence obtained on previous step through email cc&#39;ed DL: **deloittesiemhealthmonitoringteam@deloitte.com**.

Additional Troubleshooting steps:

1. While performing the above troubleshooting steps if HM team member faces any restriction like permission related issue for enabling disabling acceleration reach out to the Architecture team for additional troubleshooting support.

If Architecture Teams is unable to find root cause, then open Splunk Support case for further troubleshooting

1. HM team member updates root cause identified, solution identified, solution implemented fields on SPMAWIs
2. HM team member moves SPMAWI to closed column &amp; state
3. HM team member notifies Health Monitoring team that issue has been resolved.