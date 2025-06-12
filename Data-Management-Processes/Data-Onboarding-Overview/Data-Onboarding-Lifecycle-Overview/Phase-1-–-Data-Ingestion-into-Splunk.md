       
In this phase, onboarding of data into Splunk takes place. Here we identify the methodology to onboard the logs into Splunk. The steps are mentioned below:

**Step 6 –** Once the ticket is approved, an engineer/resource is assigned to work on the integration. The engineer to create a Project/Data Onboarding WI in Azure DevOps post assignment. (Creating a Project is not mandatory for every work item. Creating a Project is recommended to be used when there is a complex project or large number of data sources where a central work item would be helpful to have for tracking and reporting (e.g. F5 vpn onboarding)
- Engineer uses this scoping form to gather all the required information from stakeholder to start the work: [Scoping Form](https://amedeloitte.sharepoint.com/:x:/r/sites/CyberDefenseEngineering/Shared%20Documents/Data%20Management/Splunk%20Onboarding%20Document/Scoping%20Form.xlsx?d=w9d9954835bd241dea6dbefa41833e799&csf=1&web=1&e=2H8PpR)
- Updating DevOps project/Data Onboarding WI with all the parameters included in the WI type data onboarding. [DevOps Detailed Sheet](https://amedeloitte.sharepoint.com/:x:/r/sites/CyberDefenseEngineering/Shared%20Documents/Data%20Management/Splunk%20Onboarding%20Document/DevOps_WI_Fields_Review_v1.0.xlsx?d=w20c4c80a706146ef932ab49704d0fb15&csf=1&web=1&e=5NHPWg) (This sheet needs to be reviewed with Bob/Daisy before implementing the parameters)

**Step 7 –** Methodology determination on ingesting logs.
To know about details of methodologies please visit: [Data Onboarding Methodologies](https://amedeloitte.sharepoint.com/:x:/r/sites/CyberDefenseEngineering/Shared%20Documents/Data%20Management/Splunk%20Onboarding%20Document/Data%20Ingestion%20Mechanism_v.1.6.xlsx?d=w186fc743c51c46938cf892e805677b30&csf=1&web=1&e=c2pJKb)

**Step 8 –** Depending upon the data onboarding methodology, check if the required connectivity is there or not such as endpoint connectivity, S3 AWS Bucket connection, Azure repository accessibility, etc and in case of any issues take appropriate steps such as Firewall rule, S3 AWS Bucket access, Azure resources access respectively. (Please refer to the various data onboarding methodology for additional details)

**Step 9 –** Create an index in the Splunk dev indexer as per the region, example: 3 indexes could be created if it is global data in the respective DevOps branch in each region. The member firm codes are [here](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/463/Member-Firm-Country-Codes) to determine the proper MF per index naming convention.

- The objective is to onboard the data from production environment to Splunk Dev. Only in cases where there is objections from stakeholders to onboard the Prod data to Splunk Dev we will ingest the Dev data to Splunk Dev. The production data from the application/appliance/infrastructure is onboarded to Splunk production.

**Step 10 – Leveraging Cribl –** Onboarding the data through Cribl
While onboarding the logs do place the [magic parameters](https://kinneygroup.com/blog/splunk-magic-8-props-conf/) which cleans the data being onboarded from event/line breaking, headers, timestamp, etc.

**Step 11** **–** Once the data is onboarded, we leverage the **Phase 1** tab in the “**Data Quality Dashboard**” to ensure there are no line breaking, event breaking, TimeZone, latency or future timestamp issues. To maintain the sanity of data, we update our DevOps WI parameter “Data Quality Check as Passed”. Please find the link for [data quality dashboard](https://amedeloitte.sharepoint.com/:u:/r/sites/CyberDefenseEngineering/Shared%20Documents/Data%20Management/Splunk%20Onboarding%20Document/Onboarding%20guide%20documents/Data_Quality_Checker.zip?csf=1&web=1&e=5HiR1H)

Once the sanity check is done, we add a snapshot of the dashboard in the WI. If any kind of sanity issue is observed in the data, it is mentioned and highlight it in the Data Onboarding WI. Please find a sample snapshot below: 

![splunkdashboard.png](/.attachments/splunkdashboard-287bcdd7-d867-4ed5-a799-1b3407eed03d.png)


**Step 12** **–** Plugging in GEMS/GCIR/Content for review in case any net new technology is getting onboarded for data review and receiving feedback on potential data reduction. In case of existing technologies just notify GEMS.