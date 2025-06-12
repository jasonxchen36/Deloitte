The "**GEMS Splunk Data Reader SPN**" is used to ingest many different Azure data sources. The secret expires every 1 year and must be changed.

Application/Client ID: 02720f74-2949-4df4-ade0-31df9318adf3
Expiration Date: Dec/03/2025 15:35:46 PM UTC


Below is the rotation process for changing the secret.

1. Click generate new password on the [**Deloitte IAM page**](https://appreg.iam.deloitteresources.com/viewappreg?id=9757bcce-7179-a59a-d050-3b7390878611)
Note: You only have 30 seconds to view and copy the password. Afterwards you cannot view the password again.
![image.png](/.attachments/image-3523b726-4bdc-4761-a27f-0ed2c101090b.png)
2. Copy and store the new secret in Thycotic
3. Update the new secret in **Splunk**:
Change the `password.conf` file in the following servers. You need to reload the serverclass for the HFs managed by the DS. For the HFs not managed by the DS you can update the secret using the Splunk web interface.

    See this [**commit**](https://dev.azure.com/GlobalSOC/Splunk/_git/DS_Backup/commit/f6f74b5fc9a8beb5a9e8bcbf2f52c6e76c59a743?refName=refs%2Fheads%2FDS_AMER_AZURE_az1436l002&path=%2Fdeployment-apps%2FSplunk_TA_microsoft-cloudservices%2Flocal%2Fpasswords.conf&_a=compare) for example of change.

Note: The Azure NSG Flow indexes (network_azure_nsgflow_*) and Azure application indexes (application_intela_* and application_km_*) are managed by Storage Blobs and do not use the "**GEMS Splunk Data Reader SPN**" account. 

| **Region** | **Role** | **Server** | **App** | **Serverclass** | **Clients** | Index | Sourcetype| Comments |
|--|--|--|--|--|--|--|--|--|
| AMER | DS | az1436l002 | Splunk_TA_microsoft-cloudservices | all_hf_amer_microsoft_cloud_services | az1436l006 | platform_azure_activity_* | mscs:azure:activity |
| AMER | DS | az1436l002 | Splunk_TA_microsoft-cloudservices | all_hf_amer_microsoft_cloud_services | az1436l007 | application_azure_github_us | mscs:azure:github |
| AMER | DS | az1436l002 | Splunk_TA_microsoft-cloudservices | all_hf_amer_microsoft_cloud_services | az1436l076 | authentication_microsoft_entraid_all | ms:aad:signin:managedidentity, ms:aad:signin:serviceprincipal, ms:aad:signin:riskyusers | Need to remove - Migrated to Cribl |
| AMER | DS | az1436l002 | Splunk_TA_microsoft-cloudservices | all_hf_amer_microsoft_cloud_services | az1436l156 | network_azure_nsgflow_amer | mscs:nsg:flow |
| AMER | DS | az1436l002 | Splunk_TA_microsoft-cloudservices | all_hf_amer_microsoft_cloud_services | az1436l157 | network_azure_nsgflow_amer | mscs:nsg:flow |
| AMER | DS | az1436l002 | splunk_ta_o365 | all_hf_amer_o365 | az1436l005 | application_microsoft_365_* | o365:management:activity | Migrated as standalone app - Had issues in the past managed as DS |
| AMER | DS | az1436l002 | splunk_ta_o365 | all_hf_amer_o365 | az1436l006 | application_microsoft_365_* | o365:management:activity | Migrated as standalone app - Had issues in the past managed as DS |
| AMER | DS | az1436l002 | splunk_ta_o365 | all_hf_amer_o365 | az1436l007 | application_microsoft_365_* | o365:management:activity | Migrated as standalone app - Had issues in the past managed as DS |
| AMER | HF | usatramekj132 | splunk_ta_o365 | N/A | N/A | application_microsoft_365_* | o365:management:activity |
| EMEA | DS | az1436l013 | Splunk_TA_microsoft-cloudservices | all_hf_emea_microsoft_cloud_services | az1436l016 | platform_azure_diagnostic_uk | mscs:azure:datafactory, mscs:azure:diagnostic, mscs:azure:keyvault, mscs:azure:network, mscs:azure:storage |
| EMEA | DS | az1436l013 | Splunk_TA_microsoft-cloudservices | all_hf_emea_microsoft_cloud_services | az1436l077 | platform_azure_activity_* | mscs:azure:activity |
| EMEA | HF | az1436l035 | TA-microsoft-graph-security-add-on-for-splunk | N/A | N/A | platform_azure_alerts_all | GraphSecurityAlert |
| EMEA | HF | az1436l035 | Splunk_TA_MS_Security | N/A | N/A | platform_azure_alerts_all | ms:defender:atp:alerts |
| APAC | DS | az1436l021 | Splunk_TA_microsoft-cloudservices | all_hf_apac_microsoft_cloud_services | az1436l022 |  application_intela_mongodb_apactax | mongodb:audit, mongodb:authentication |
| APAC | DS | az1436l021 | Splunk_TA_microsoft-cloudservices | all_hf_apac_microsoft_cloud_services | az1436l022 |  application_km_admin_apactax | km:admin:auth |
| APAC | DS | az1436l021 | Splunk_TA_microsoft-cloudservices | all_hf_apac_microsoft_cloud_services | az1436l022 |  application_km_hvur_apactax | km:hvur |
| APAC | DS | az1436l021 | Splunk_TA_microsoft-cloudservices | all_hf_apac_microsoft_cloud_services | az1436l050 |  platform_azure_activity_* | mscs:azure:activity |
| APAC | DS | az1436l021 | Splunk_TA_microsoft-cloudservices | all_hf_apac_microsoft_cloud_services | az1436l051, az1436l163, az1436l164 |  network_azure_nsgflow_apac | mscs:nsg:flow |

4. Update the new secret in **Cribl**:
a. Navigate to Worker Groups > amer_azure_prod > Data > Sources > Azure Event Hubs
![image.png](/.attachments/image-3bbab785-df9c-4a5d-8287-5d22a3be3c42.png)
b. Click on the **Event Hub input** that needs modified and go to **Authentication**
![image.png](/.attachments/image-ca2d8c2a-4288-45ac-8656-89d0a9e9c4a5.png)
c. Update the **Client Secret** and click **Save**
d. Click on the **Commit** button, write a commit message and then click on **Commit & Deploy** to push the change


| Worker Group | Input ID | Brokers | Topic | Index | Sourcetype |
|--|--|--|--|--|--|
| amer_azure_prod | global_aad_audit | azuseeenthub-amer-splunk.servicebus.windows.net:9093 | insights-logs-auditlogs | authentication_microsoft_entraid_<region> | ms:aad:audit |
| amer_azure_prod | global_aad_managedidentity | azeusAADSPLprdehb02.servicebus.windows.net:9093 | insights-logs-additionalsignin01 | authentication_microsoft_entraid_<region> | ms:aad:signin:managedidentity, ms:aad:signin:serviceprincipal |
| amer_azure_prod | global_aad_riskyusers | azeusAADSPLprdehb02.servicebus.windows.net:9093 | insights-logs-riskalerts | authentication_microsoft_entraid_<region> | ms:aad:signin:riskyusers |
| amer_azure_prod | global_aad_signin | azeusAADSPLprdehb01.servicebus.windows.net:9093 | insights-logs-signinlogs | authentication_microsoft_entraid_<region> | ms:aad:signin |
| amer_azure_prod | global_azure_github | azuseGITSPLprdehb01.servicebus.windows.net:9093 | insights-logs-githublogs2 | application_azure_github_<region> | mscs:azure:github |
| emea_azure_prod | Global_Microsoft_Defender_UrlClickEvents | azeunCPSSPLprdehb01.servicebus.windows.net:9093 | insights-logs-advancedhunting-urlclickevents | email_microsoft_defender_<region> | mscs:azure:eventhub:defender:advancedhunting |
| emea_azure_prod | Global_Microsoft_Defender_EmailPostDeliveryEvents | azeunCPSSPLprdehb01.servicebus.windows.net:9093 | insights-logs-advancedhunting-emailpostdeliveryevents | email_microsoft_defender_<region> | mscs:azure:eventhub:defender:advancedhunting |


5. Validate the inputs that use updated SPN secret and are functioning correctly.

Note: The indexes (_authentication_microsoft_entraid_*_, _application_microsoft_365_*_, _application_azure_github_*_, _email_microsoft_defender_*) are pulled from a global event hub and then split up into different regional indexes (all, amer, emea, apac) using Cribl. The "all" index is designated as a catch-all index if the user_work_country field cannot be identified.

**AMER:**
`| tstats max(_time) as latestTime max(_indextime) as latestIndexTime count WHERE index IN (platform_azure_activity_*, network_azure_nsgflow_amer, authentication_microsoft_entraid_all, authentication_microsoft_entraid_amer, application_microsoft_365_all, application_microsoft_365_amer, application_azure_github_us, application_azure_github_all, application_azure_github_amer, email_microsoft_defender_amer) by index, sourcetype, host | convert ctime(latestTime) | convert ctime(latestIndexTime)`


**EMEA:**
`| tstats max(_time) as latestTime max(_indextime) as latestIndexTime count WHERE index IN (platform_azure_activity*, network_azure_nsgflow_emea, platform_azure_alerts_all, platform_azure_diagnostic_uk, authentication_microsoft_entraid_emea, application_microsoft_365_emea, application_azure_github_emea, email_microsoft_defender_all, email_microsoft_defender_emea) by index, sourcetype, host | convert ctime(latestTime) | convert ctime(latestIndexTime)`

**APAC:**
`| tstats max(_time) as latestTime max(_indextime) as latestIndexTime count WHERE index IN (platform_azure_activity*, network_azure_nsgflow_apac, authentication_microsoft_entraid_apac, application_microsoft_365_apac, application_azure_github_apac, email_microsoft_defender_apac, application_km_hvur_apactax, application_km_admin_apactax, application_intela_mongodb_apactax) by index, sourcetype, host | convert ctime(latestTime) | convert ctime(latestIndexTime)`

