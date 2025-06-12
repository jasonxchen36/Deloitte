# **Playbook: DMC Alert - Splunk Support SHC member out of synch**

An alert from the Distributed Monitoring Console (DMC) is triggered due to an acceleration running in a non-approved app. This should be disabled at earliest convenience.

Health Monitoring Alert Work Item (HMAWI) is automatically created by Azure Logic and added to Health Monitoring Team board on the &quot;New&quot; column. Also, an email is sent to **deloittesiemhealthmonitoringteam@deloitte.com**

HMAWI is automatically populated with alert name, issue, playbook steps and/or link to playbook, date created, and associated SLA time for resolution

HM team assign HMAWI work item to available HM team member 

HM team lead is responsible for managing HM team member workload to make sure resolution can be met within SLA

HM team member starts resolution process by following alert-specific playbook

**Playbook: DMC Alert - Splunk Support SHC Member out of Synch**

DMC Alert - Splunk Support SHC member out of synch:

1. HM team member moves HMAWI to &quot;Active&quot; column on HM Team board
2. HM team member accesses Splunk GUI and verifies the veracity of the triggered alert by running the following query and checking if results are the same as the received on the HMAWI:
```
_index=_internal ((host=usatramekj003) OR (host=usatramekj002) OR (host=usatramekj100) OR (host=usatramekj101) OR (host=usatramekj001)) 
source="*splunkd.log*" NOT "SearchOperator:kv" "Error pulling configurations from captain" earliest=-60m   
| stats max(consecutiveErrors) AS consecutive_count by host    
| where  consecutive_count>500
```
When finished with above steps, HM team member will follow the steps provided below:

1. Check the host name.

![image.png](/.attachments/image-b81defb0-328b-4fbb-9e2b-15a8296f9619.png)

2. Go to Settings -> Search Head Clustering. If you see a host with a status is down, Please go ahead and drop an email to Global FC Engineering Team [**deloittesiemhealthmonitoringteam@deloitte.com**](mailto:deloittesiemhealthmonitoringteam@deloitte.com) and proceed with the investigation why the search head is down. Try checking &quot;Splunk server&quot; is running logging in background of Search head.

 ![](RackMultipart20200630-4-zcnumi_html_40f3eedead7afce5.png)
3. Check of the mentioned host is able to access. If yes, click the &quot; i&quot; icon beside your login name to see this page. If you see a Red mark beside any of Search head related things, Notify the Health Monitoring Team and continue to investigate of the cause.

![image.png](/.attachments/image-4c053c7e-5a6b-4ce0-80ae-5f4da73c1895.png)

4. After completing Troubleshooting and resolving the problem, Then HM team Member will move the HMAWI to &quot;Closed&quot; and inform the stake holder/creator with the evidence obtained on previous step through email cc&#39;ed DL: **deloittesiemhealthmonitoringteam@deloitte.com**.

6.	Additional Troubleshooting steps If Issue still exists:

   In case, while performing the above troubleshooting steps if HM team member faces any restriction like permission related issue for enabling disabling acceleration reach out to the Engineering team for additional troubleshooting support.

If Architecture  team is unable to find root cause, then open Splunk Support case for further troubleshooting. When the solution is identified, HM team member updates the HMAWI to appropriate states (root cause identified, solution identified, solution implemented fields) on HMAWIs.

7.	Then the HM team member moves HMAWI to closed column & state and notifies Health Monitoring that issue has been resolved.
