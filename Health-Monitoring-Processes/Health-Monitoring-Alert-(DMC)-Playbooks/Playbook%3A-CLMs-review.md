CLMs Playbook
=================

## Objective
---------

This document outlines the standardized procedures for daily monitoring, troubleshooting, escalation, and resolution of CLM-related alerts. The goal is to promptly identify issues, take appropriate actions, and ensure efficient resolution.



## 💡 **1.** **Daily Monitoring of CLMs**
---------------------------

Every day, verify the status of CLMs in each environment:
*   **EMEA & AMER:** [Splunk EMEA/AMER CLM Check](https://es-dt-emea.splunkcloud.com/en-US/app/search/clm_check)
    
*   **APAC:** [Splunk APAC CLM Check](https://es-dt-apac.splunkcloud.com/en-US/app/search/clm_check)
    
Ensure the dashboard shows **no results** (empty status). An empty status indicates that all CLMs are properly sending data.

 ✅  **Healthy Example:** "No results found for CLMs stopped sending data in the last hour."
> ![Picture1.png](https://dev.azure.com/GlobalSOC/93d9ecc1-89fd-4a34-a69b-7282df6fad64/_apis/git/repositories/7c3c331d-0fac-420a-9ad2-1a920f9247d9/Items?path=/.attachments/Picture1-a9a52434-c5b9-4085-88c5-69f09d0f1598.png&download=false&resolveLfs=true&%24format=octetStream&api-version=5.0-preview.1&sanitize=true&versionDescriptor.version=wikiMaster)
    
⚠️ **AMER** frequently shows _**delays**_; allow a tolerance window of **2-3 hours**. 
- Beyond this threshold, take immediate action.
>![Picture2.png](https://dev.azure.com/GlobalSOC/93d9ecc1-89fd-4a34-a69b-7282df6fad64/_apis/git/repositories/7c3c331d-0fac-420a-9ad2-1a920f9247d9/Items?path=/.attachments/Picture2-c5d5f510-a821-4417-ab9b-1f9bb7720f3d.png&download=false&resolveLfs=true&%24format=octetStream&api-version=5.0-preview.1&sanitize=true&versionDescriptor.version=wikiMaster)

## 📌 Special Cases

   **IPs starting with 10.30.9.12:** Managed internally by Canada (CA) MF team. **No ticket required.**
>![Picture3.png](https://dev.azure.com/GlobalSOC/93d9ecc1-89fd-4a34-a69b-7282df6fad64/_apis/git/repositories/7c3c331d-0fac-420a-9ad2-1a920f9247d9/Items?path=/.attachments/Picture3-c8707204-52cf-428e-84f1-5d740a93a505.png&download=false&resolveLfs=true&%24format=octetStream&api-version=5.0-preview.1&sanitize=true&versionDescriptor.version=wikiMaster)
* * *

## 🔍 **2. Syslog/Queue Data Verification**
* * *

**Before sending the notification email or escalating further:**
1.  **Check the relevant syslog hosts** (can be MF-owned or Splunk-owned; see ([Queue blockages](https://shc1.pvt.dt-emea.splunkcloud.com/en-US/app/search/search?q=search%20index%3D_internal%20source%3D*metrics.log%20group%3Dqueue%20host%20IN%20(%E2%80%A6)%20earliest%3D-2h%0A%7C%20stats%20max(current_size)%20AS%20max_q%20by%20host%2Cname%0A%7C%20where%20max_q%3E0&sid=1749136116.3229_6BCFE5CC-E108-454E-B400-6193D504FABB&display.page.search.mode=smart&dispatch.sample_ratio=1&earliest=-30m%40m&latest=now))).
    *   Use the quick links in Section 6 or run a Splunk search such as for logs in the **last 2 hours**.: 
> `index=_internal host IN (EU1436L041,EU1436L042 (or, depending on region) az1436l163,az1436l164) earliest=-2h`

2.  **If recent logs are present:**
    *   Investigate for possible **queue blockages** (e.g., data sent but not indexed).
        
    *   Review Splunk ingestion logs, UF queues, and error messages.
        
    *   Escalate only if you confirm a **real queue/data blockage** or ingestion issue.
        
3.  **If no recent logs are found:**
    *   Proceed with escalation as planned (move onto Step 3).
        

> _Why this step?_  
> Sometimes CLMs are sending data, but downstream issues (such as queue blockages) prevent ingestion. Checking this early avoids unnecessary escalations and focuses troubleshooting.
        

* * *
## 📝 **3. ServiceNow Ticketing Procedure**
---------------------------------

If the CLM is down beyond the allowed threshold, follow these steps:

### Step 1: Determine Ownership

-  **US, Canada, Switzerland, S-Latam, Mexico, and Israel CLMs**: Do **not** escalate to the FW team. 
>Contact respective MF points of contact (POCs).
    

### MF Points of Contact

>   **Latco & Mexico:**
      Martha Brenda Flores: [martflores@deloittemx.com](mailto:martflores@deloittemx.com)
        Patricio Mercado: [pmercado@deloittemx.com](mailto:pmercado@deloittemx.com)
        
>   **Switzerland:**
      Philipp Campisi: [pcampisi@deloitte.ch](mailto:pcampisi@deloitte.ch)
        
>   **Canada & Chile:**
 Michael Fraser: [mifraser@deloitte.ca](mailto:mifraser@deloitte.ca)
        Timothea Reynders: [treynders@deloitte.ca](mailto:treynders@deloitte.ca)
        
>   **IL & US Firewall Operations:**
    [dtusfirewalloperations@deloitte.com](mailto:dtusfirewalloperations@deloitte.com)
        

### Step 2: Creating a ServiceNow Ticket

*   [Create a new ServiceNow ticket](https://deloitteglobal.service-now.com/incident.do?sys_id=-1&sysparm_query=active=true)
    
*   Fill out mandatory fields per guidelines:
    *   Environment (AMER/APAC/EMEA)
        
    *   Affected CLM IP and name
        
    *   Impact description (**Urgency**)
> Sample ticket: INC1937438

>![Picture4.png](https://dev.azure.com/GlobalSOC/93d9ecc1-89fd-4a34-a69b-7282df6fad64/_apis/git/repositories/7c3c331d-0fac-420a-9ad2-1a920f9247d9/Items?path=/.attachments/Picture4-0e01bddc-d8b1-4b94-bf5e-ce2f558ac650.png&download=false&resolveLfs=true&%24format=octetStream&api-version=5.0-preview.1&sanitize=true&versionDescriptor.version=wikiMaster)

* * *

## 📧 **4. Email Notification Procedure**
-------------------------------

After creating the SNOW ticket, immediately initiate an email thread for incident tracking:
**Subject:** (AMER/APAC/EMEA) CLM DOWN – INCxxxxx
**To:**
*   **Primary Firewall Team Contacts**
_Teams below are distribution lists, emails end in @deloitte.com_
   GTS GTI Firewall Management Services Operations
   GTS GTI Firewall Management Services Architecture
    
**CC:** Deloitte SIEM Health Monitoring Team
**Email Template:**

    Hi Team,
    
    The following CLM is down:
    
    Environment: AMER
    network_checkpoint_firewall_ca - 10.254.39.180
    
    Could you please restart the CLM and confirm once done?
    
    Incident Reference: INCxxxxx
    
    Thanks in advance.
    

* * *

## **🛑 5. Escalation for Multiple CLMs Down**
------------------------------------

If **multiple** CLMs remain down after the initial restart:
1.  Open a [Checkpoint Firewall Escalation Ticket](https://deloitteglobal.service-now.com/sp?id=sc_cat_item&sys_id=01425218373faa048747579543990e98).
    
2.  If the situation is critical (business-impacting):
    *   Create the ticket.
        
    *   Include **TOC & GTS GTI Firewall Management Services Engineering** in the trailing email thread. 
(_note this_ "**Engineering DL**" _should only be used to escalate potential Checkpoint Issues_")
        
    *   **TOC** will escalate to Firewall Engineering on-call for urgent resolution.
        

* * *

## **6. Syslog Server Verification**
-----------------------------

Verify logs availability on syslog servers to assist in troubleshooting:
    
*   **EMEA & AMER Syslog Servers:** [EMEA & AMER Checkpoint Syslog Check](https://es-dt-emea.splunkcloud.com/en-US/app/search/search?q=search%20index%3D_internal%20host%20IN%20(%22EU1436L041%22%2C%22EU1436L042%22)%20%7C%20head%2010&display.page.search.mode=smart&dispatch.sample_ratio=1&earliest=-30m%40m&latest=now&sid=1749115485.9244_54C0E99A-0006-40BB-8D32-E7A28725447B)
    
*   **APAC Syslog Servers:** [APAC Checkpoint Syslog Check](https://es-dt-apac.splunkcloud.com/en-US/app/search/search?q=search%20index%3D_internal%20host%20IN%20(%22az1436l163%22%2C%22az1436l164%22)%20%7C%20head%2010&display.page.search.mode=smart&dispatch.sample_ratio=1&earliest=-30m%40m&latest=now&sid=1749115577.22920_3D4518BD-F27E-4075-A74F-A6861FA31E6E)
    

* * *

## **7. General Escalation Workflow (Non-Splunk vs. Splunk Issues)**
-------------------------------------------------------------

### Non-Splunk Issues:

1.  Notify stakeholders and relevant **MF** POCs.
    
2.  Clearly communicate via existing email thread.
    
3.  Escalate to **GEMS team** for awareness.
    

### Splunk-Related Issues:

1.  Continue troubleshooting and remain engaged.
    
2.  Confirm resolution via email once fixed.
    
3.  Escalate to Splunk Support if necessary (reference [Splunk Cloud SOP](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/1052/Splunk-Cloud-SOP)).
    

* * *

##🔗 **Additional Resources**
-----------------------

*   [Splunk Cloud SOP Overview](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/1052/Splunk-Cloud-SOP)
    
*   [ServiceNow Home Page](https://deloitteglobal.service-now.com/)
    
*   [MF Contacts List](https://amedeloitte.sharepoint.com/:x:/r/sites/GEMSSIEMEngineering/_layouts/15/Doc.aspx?sourcedoc=%7BD881E344-235A-476E-8A7E-DDE7AF41AB51%7D&file=CyberDefenseMFContactList.xlsx)

* Expert in leading Checkpoint cases, rriddle@deloitte.com
    

* * *

**Note:** Always verify if the issue is Splunk or external (MF) related. Escalate according to these guidelines to ensure timely resolution.