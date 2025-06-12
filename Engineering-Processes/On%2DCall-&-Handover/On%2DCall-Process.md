On-Call Process for MF P1 Escalations
=====================================

This page outlines the **updated on-call process** for handling MF P1 escalations within the CDE on-call team. We will continue to add P1s to the P1 escalation list, and certain issues may require **MF** escalation via the **GEMS** team. The on-call engineer’s primary responsibility is to **prioritize response** and **verify Splunk-side functionality**.

* * *
 
## 1. Overview
-----------

*   **CDE On-Call Team** will handle MF P1 incidents the same as existing P1s.
*   Acknowledge the **P1 phone call** promptly and begin initial triage.
*   Determine if the incident is **Splunk-related** or **external (MF) related**.

* * *

## 2. Handling MF P1 Incidents
---------------------------

### 2.1 Non-Splunk Issues

If upon investigation the root cause does **not** lie within Splunk (e.g., MF-side misconfiguration, external dependency, etc.):
1.  **Notify the Appropriate Stakeholders**
    *   Send an email to the relevant POCs (per **POC list/SOP**).
    *   Create a **ServiceNow** ticket if needed.
2.  **Communicate Clearly**
    *   Reply to the existing email thread (including GEMS) stating that Splunk checks are clear and the issue is **outside Splunk’s control**.
3.  **GEMS Escalation**
    *   **GEMS** will determine next steps (e.g., escalate to **TOC** or **MF** teams).
    *   **TOC/MF** may re-engage the on-call engineer if additional Splunk assistance is required once MF resources are involved.

### 2.2 Splunk-Related Issues

If investigation confirms the issue **is** Splunk-related:
1.  **Continue Troubleshooting**
    *   The on-call engineer remains engaged until the issue is resolved.
2.  **Confirm Resolution**
    *   Once resolved, reply to the email thread confirming that the problem was Splunk-related and has been fixed.
3.  **Splunk Support Cases**
    *   **Open a Splunk Support case** during on-call hours **only** if needed, referencing the [Splunk Cloud SOP - Overview](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/1052/Splunk-Cloud-SOP) for guidelines on when to escalate externally.

***

## 3. GEMS & MF Escalation Workflow
--------------------------------

*   **GEMS** triages non-Splunk issues and decides if **TOC** or **MF** involvement is required.
*   If TOC or MF are engaged, they may **loop in** the on-call engineer again for collaborative troubleshooting.

* * *

##4. References
-------------

*   [Splunk Cloud SOP - Overview](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/1052/Splunk-Cloud-SOP)
*   [ServiceNow Ticketing Procedures](https://deloitteglobal.service-now.com/now/nav/ui/classic/params/target/incident.do%3Fsys_id%3D-1%26sysparm_query%3Dactive%3Dtrue%26sysparm_stack%3Dincident_list.do%3Fsysparm_query%3Dactive%3Dtrue)
* [Firewall Ticketing Procedures](https://deloitteglobal.service-now.com/sp?id=sc_cat_item_guide&sys_id=504f4d79c3495210bdf4744ed4013155)
* [CLMs Playbook - Overview](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/1005/Playbook-CLMs-review)
* [POC List](https://amedeloitte.sharepoint.com/:x:/r/sites/GEMSSIEMEngineering/_layouts/15/Doc.aspx?sourcedoc=%7BD881E344-235A-476E-8A7E-DDE7AF41AB51%7D&file=CyberDefenseMFContactList.xlsx&wdLOR=cB4FEB6F4-28F5-44EE-A3B2-FD0A1D449211&action=default&mobileredirect=true&CID=6BAB5BA1-44EA-40DF-830A-B63FC197F8A6)


* * *

**Note**: Always confirm whether an issue originates in Splunk or not. If it’s clearly Splunk-related, continue troubleshooting and escalate to Splunk Support if necessary. If it’s outside Splunk’s scope, hand off to GEMS/TOC/MF per the guidelines above.