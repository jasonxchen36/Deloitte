       
Once everything is tested, validated, and completed about the data we onboarded in Splunk Dev environment, it becomes production ready. Now we push the data in production where actual contents runs on the data and alerts are generated for the Security Operations Centre (SOC) and IR (Incident Response) teams. To push data into production we must follow a series of steps mentioned below:

**Step 18 –** Deployment of inputs into both staging and production as Staging do not have separate set of infrastructure of HF or indexer. (UF,HF,Syslog).
- Create one or multiple Pull Request into the respective Indexer branch depending on the number of indexes that is needed as per the data source region (on-prem, cloud) of the region where we would want to be reflected.
- The index that will be created will serve for both staging and production as there is no separate branch for stage and production.
- Add the index name in “**Splunk_SA_CIM**” for plug-in the feed with respective data model and update the “**Updated Data Model Macro**” parameter in the Data Onboarding WI as “Yes”. Add the snapshot in the Data Onboarding WI.
- Update the parameter “**Health Monitoring – Index Mapping Lookup**” in the Data Onboarding WI ensure that the index is added for HM by adding it into the lookup **index_mapping.csv** and place a snapshot after the index is added.

![splunksearch1.png](/.attachments/splunksearch1-239db769-6de3-4482-b906-729006ac536e.png)

![splunksearch2.png](/.attachments/splunksearch2-45cce6d0-2fbf-4685-b9d6-29196b44e122.png)

- **AppSec Specific** – Update the parameter “**AppSec Content Lookup**” in the Data Onboarding WI to ensure we are adding the index to application security content monitoring by adding it into the lookup **application_security_indexes**, take a snapshot and place it in the WI.

![splunksearch3.png](/.attachments/splunksearch3-bacdd075-07e5-4f1b-ba65-3072fc6dc472.png)

**Step 19 –** Deploy all search-time extractions as an App or a TA via Pull Request into the staging environment to see if everything reflects as expected.
- The TA or the App can have any number of .conf files under correct folder, but some of the mandatory files and folders are **readme.txt, app.conf, metadata and default.**
- Once everything is proper in the Stage environment, proceed for the production push.

**Step 20** **–** Create Pull Request to push the search-time configurations into Splunk production.

**Step 21** **–** Once the data is in production, please check the data with the help of Data Quality App in the prod using both the tabs “Phase 1” & “Phase 2”and take a screenshot and attach to DQ WI.

**Step 22** **–** If the data quality is in line with the expectation proceed for documentation and notification.

**Step 23 –** In case of any data quality issues, please address the issue or document it well before sending notification.

![splunkdashboard1.png](/.attachments/splunkdashboard1-d711da5d-09f2-4319-9f38-b9408347bf83.png)

- To know how to create a pull request please visit here: [Pull Request creation](https://amedeloitte.sharepoint.com/:w:/r/sites/CyberDefenseEngineering/Shared%20Documents/Data%20Management/Splunk%20Onboarding%20Document/Onboarding%20guide%20documents/Creation%20of%20Pull%20Request%20_new.docx?d=w0d525b74635b405c90dded6361751f21&csf=1&web=1&e=PPSTs1)
- To know the schedule of push into various branches please visit: [Change Schedule](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/641/AMER-EMEA-APAC-Splunk-Production-and-Staging-Change-schedule)