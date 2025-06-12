The following outlines the common Splunk and ServiceNow searches to satisfy audit requests:

**Assets Reporting in Splunk:** 
- Go to the Search Head of the appropriate region for the MF requesting the audit 
- Run the following searches using the Specific Member Firm Identifier, Region (US and AMER are used in this example), and if specific hostnames were provided: 
- [ ] On Prem:`| tstats count where index=us_*windows* OR index=us_*nix* by host, index`
- [ ] Cloud: `| tstats count where index=amer_*windows* OR index=amer_*nix* host=us* by host, index`
- [ ] Specific Host: `| tstats count where index=*windows* OR index=*nix* host IN(hostname1, hostname2, hostname3) by host`

**Alert generation in Splunk:** 
- Go to the Search Head of the appropriate region for the MF requesting the audit (usually AMER provides the most results)
- Run the following search with Specific MF Identifier (US is used in this example): `index=notable NOT search_name=*DEV* orig_index=us_* | stats count by search_name` 
- To look up specific alert example include the specific alert name under "search_name": `index=notable NOT search_name=*DEV* orig_index=us_*  search_name="Threat - FC-014-Suspicious IP Address Observed in Web Data - Netskope-AMER - Rule"`

**List of content items:** This request requires approval from leadership prior to sharing, please reach out to Daniel Azrak (dazrak@deloitte.com).
- Run this query in DevOps to pull the latest list of Closed Build Content Tasks: https://dev.azure.com/GlobalSOC/Splunk/_queries/query-edit/168d6b58-2c3d-48cc-89a6-b08a1c7950a3/

**Content rule configurations:** This request requires approval from leadership prior to sharing, please reach out to Daniel Azrak (dazrak@deloitte.com). 
- This request can be pulled via DevOps and exported to CSV by utilizing the field for Search Query Logic: https://dev.azure.com/GlobalSOC/Splunk/_queries/query-edit/168d6b58-2c3d-48cc-89a6-b08a1c7950a3/.
- The configurations can also be shown in a walkthrough via savedsearches.conf and any evidence requests can be screenshotted and provided once approved. 

**365 Day Retention:** 
- Go to this link and screenshot rows 56 to 73: https://dev.azure.com/GlobalSOC/Splunk/_git/IndexerCM?path=/del_amer_prod_all_indexes/local/indexes.conf&version=GBICM_AMER_RDC&_a=contents

**List of indexes/data type:** 
- Go to the Search Head of the appropriate region for the MF requesting the audit 
- Run the following search using the Specific Member Firm Identifier or Region (US is used in this example):`| tstats count where index=us_* by index`

**Security Monitoring Alerts:** 
- Run this query in DevOps to pull the latest list of Closed Security Monitoring Alerts in the last 7 days: https://dev.azure.com/GlobalSOC/Splunk/_queries/query-edit/e71d59ed-5647-4864-b2ec-6c3e05d049e6/

**Health Monitoring Alerts:** 
- Run this query in DevOps to pull the latest list of Closed Data Monitoring Alerts in the last 7 days: https://dev.azure.com/GlobalSOC/Splunk/_queries/query-edit/c966187c-26c0-4745-a9c3-f0226c7bd89d/

**Access Review/Control Process:** 
- Refer to our Semi-Annual Access Review Process documented here in Section 2: https://amedeloitte.sharepoint.com/:w:/r/sites/CyberDefenseEngineering/Shared%20Documents/Process/Process%20Documentation/Annual%20Review/Cyber%20Defense%20Engineering%20Annual%20Review%20v1.7.docx?d=wf56fac79ea004f5d9ca0ef80e85b47c8&csf=1&web=1&e=vJw9bd
- The Semi-Annual Access Review evidence is stored in this Teams folder. Reference the document titled "Cyber Defense Engineering_Members_Review": https://amedeloitte.sharepoint.com/:f:/r/sites/CyberDefenseEngineering/Shared%20Documents/Process/Process%20Documentation/Annual%20Review?csf=1&web=1&e=XxsbzA

**Capacity Tracker:** 
- Refer to this Excel Document link to show the monthly capacity trends and tracking: https://amedeloitte.sharepoint.com/:x:/s/DeloitteHealthMonitoring/ESbyieq8lSVIhuYoih0rqPkBsk14hvuV510Fz8sOMRLqJw?e=4%3As8ICuA&fromShare=true&at=9&CID=33F86AF8-7345-4258-A3F8-59369816F9E4&wdLOR=cD47BD3D6-3641-4177-A09D-B41E4F29A93C



**Alert and SIR details in ServiceNow**: 
_Note: For any of the following ServiceNow export or evidence requests please reach out to Katherine Khusial (kkhusial@deloitte.com) to provide._ 
- Go to the following link to search for Security Incidents in ServiceNow and include the specific Member Firm country if required: 
https://deloitteglobal.service-now.com/now/nav/ui/classic/params/target/sn_si_incident_list.do%3Fsysparm_query%3D%26sysparm_first_row%3D1%26sysparm_view%3DCyber

![ServiceNow Ticket Search.png](/.attachments/ServiceNow%20Ticket%20Search-809edacf-f7f7-4b51-833b-9608d37b3ee9.png)
- Click the SIR Number details to open up the specific ServiceNow SIR Ticket for more information
- For an export of ServiceNow SIR tickets, please reach out to Katherine Khusial (kkhusial@deloitte.com) to provide and redact any sensitive information
