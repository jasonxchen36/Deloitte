Repository of all the dashboard that we have developed in the environment to met requirements of the teams internal/external


| **Dashboard Name** | **Dashboard link** | **Splunk App** | **Coverage**| **Description** |
|--|--|--|--|--|
|MITRE ATT&CK Framework| https://amersplunk.atrame.deloitte.com/en-US/app/DA-ESS-MitreContent/mitre_attck_deloitte_compliance | DA-ESS-MitreContent || This dashboard provides an overview of available correlation searches and technologies that match MITRE ATT&CK techniques |
|Data Quality Phase 1/Data Quality Phase 2| https://amersplunk.atrame.deloitte.com/en-US/app/Data_Quality_Checker/data_quality_dashboard | Data_Quality_Checker | AMER/EMEA/APAC |This dashboard is to facilitate CIM (Common Information Model) validation within Splunk. It ensures that onboarded data adheres to CIM compliance standards as outlined in the Appsec required field document. |
||https://amersplunk.atrame.deloitte.com/en-US/app/Global_FC_Monitoring/Content_Management_Monitoring | Global_FC_Monitoring | |Quick overview of the content that we have deployed and enabled in our environment including a few useful metrics regarding content volume.
|Application/Infrastructure Security Contact Information|https://emeasplunk.atrame.deloitte.com/en-US/app/SOC_Escalation/security_contact_information | SOC_Escalation | AMER/EMEA/APAC |This dashboard provides a holistic picture of the Point of contacts. As for content escalation, SOC needs to choose “Content Escalation Contact/Email”. Similarly for data feed issue Health Monitoring team needs to choose “data Feed Issue Contact/Email”. BISO team needs to be mentioned in both aforesaid cases for awareness. |
|Application Security Overview |https://emeasplunk.atrame.deloitte.com/en-US/app/application_security_datasources/home | application_security_datasources | AMER/EMEA/APAC |This dashboard is mainly used for getting contact details for Application and Infrastructure indexes with following information : Biso Contact, Content Escalation Contact, Data Feed issue contact. |
| User Data Access NTK Dashboard |https://amersplunk.atrame.deloitte.com/en-US/app/SplunkEnterpriseSecuritySuite/user_data_access_ntk | Enterprise Security | AMER/EMEA/APAC | The User Data Access dashboard is the only acceptable way for user data to be accessed in Splunk. Click [here](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/162/User-Data-Access-NTK-Dashboard) for more information.
| Missing Data In Indexes |https://es-dt-emea.splunkcloud.com/en-US/app/SplunkEnterpriseSecuritySuite/Missing_data_in_indexes | Enterprise Security | AMER/EMEA/APAC | Map indexes that don't have live data, and last time data was ingested.
| User Response Dashboard | https://es-dt-emea.splunkcloud.com/en-US/app/search/ess_user_across_dm | Enterprise Security | AMER/EMEA/APAC | This dashboard is mainly used to search the activity related with an specific user across all DM.
| IAM Dashboard | https://es-dt-emea.splunkcloud.com/en-US/app/IAM_Dashboard/IAM_DB | IAM Dashboard App | AMER/EMEA/APAC | The purpose of IAM Dashboard is to provide meaningful and actionable insights using metrics, performing analytics and doing Prediction on Deloitte MFs security risk posture that will help stakeholders to make informed and proactive decisions aim to drive change (people, process and technology).
| Incident Investigation Dashboard | https://amersplunk.atrame.deloitte.com/en-US/app/Global_FC_Monitoring/incident_investigation_dashboard | Global FC Monitoring Content | AMER/EMEA/APAC | The purpose of IID Dashboard is to help analysts to detect suspicious activities around specific host/user.
| Brute Force Dashboard | https://amersplunk.atrame.deloitte.com/en-US/app/Global_FC_Monitoring/Brute_force_dashboard | Global FC Monitoring Content | AMER/EMEA/APAC | The purpose of BruteForce Dashboard is to provide insights on brute force kind of activities.






