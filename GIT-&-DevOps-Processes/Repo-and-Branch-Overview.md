_[[_TOC_]]_
Below are the the branch descriptions that exist for the AMER, EMEA and APAC Splunk environments. All the branches are in its respective repo category. 



**Search Head Cluster Deployer**
---
Repo: SHC
Deploys to: /opt/splunk/etc/shcluster/apps/ 
_Only for AMER. APAC and EMEA pushes are made through Splunk ACS_

**Branch** | Description| **Notes**
---|-----|------
SHC_AMER|Production branch for SHC AMER region|
SHC_AMER_STAGING|Staging branch for SHC AMER region|
SHC_AMER_DEV|Development branch for SHC AMER region|
SHC_AMER_FCMA|Metrics team AMER production branch |Deploys to /opt/splunk/etc/apps since this is a stand-alone search head
SHC_EMEA|Production branch for the SHC EMEA region|
SHC_EMEA_STAGING|Staging branch for SHC EMEA region| **Deprecated. No staging environment after Cloud migration.** 
SHC_EMEA_DEV|Development branch for SHC EMEA region|
SHC_EMEA_AZURE|Production branch for Global SHC located in EMEA Azure region| **Deprecated. No Global environment after Cloud migration.** 
SHC_EMEA_STAGING_AZURE|Staging branch for Global SHC located in EMEA Azure region| **Deprecated. No staging environment after Cloud migration.** 
SHC_APAC|Production branch for SHC APAC region |
SHC_APAC_STAGING|Staging branch for SHC EMEA region| **Deprecated. No staging environment after Cloud migration.**
SHC_APAC_DEV|Development branch for SHC APAC region|

---

Repo: SHD_Backup
Backs up: /opt/splunk/etc/apps, /opt/splunk/etc/shcluster and opt/splunk/etc/system/local every hour.

**Branch** | Description| **Notes**
---|-----|------|
SHD_AMER_usatramekj042|Production branch backup for usatramekj042||
SHD_APAC_ap1436l021|Production branch backup for ap1436l021|**Deprecated.**|
SHD_EMEA_AZURE_az1436l055|Production branch backup for az1436l055||
SHD_EMEA_eu1436l021|Production branch backup for eu1436l021||


**Indexer Cluster Master**
---
Repo: IndexerCM
Deploys to: /opt/splunk/etc/master-apps
 
**Branch** | Description| **Notes**
---|-----|------
ICM_AMER|Production branch for ICM in the AMER region|
ICM_AMER_DEV|Development branch for ICM in the AMER region|
ICM_AMER_AZURE|Production branch for ICM in the AMER Azure region|
ICM_AMER_DEV_AZURE|Development branch for ICM in the AMER Azure region|
ICM_AMER_AWS|Production branch for ICM in the AMER AWS region|
ICM_AMER_DEV_AWS|Development branch for ICM in the AMER AWS region|
CM_US|Production branch for ICM in the US region|**Deprecated.**
ICM_EMEA|Production branch for ICM in the EMEA region|**Deprecated. Indexes are managed in SHC_EMEA branch.**
ICM_EMEA_AZURE|Production branch for ICM in the EMEA Azure region|**Deprecated. Indexes are managed in SHC_EMEA branch.** 
ICM_EMEA_DEV_AZURE|Development branch for ICM in the EMEA Azure region|**Deprecated. Indexes are managed in SHC_EMEA_DEV branch.**
ICM_EMEA_AWS|Production branch for ICM in the EMEA AWS region|**Deprecated. Indexes are managed in SHC_EMEA branch.**
ICM_EMEA_DEV_AWS|Development branch for ICM in the EMEA AWS region|**Deprecated. Indexes are managed in SHC_EMEA_DEV branch.**
ICM_APAC|Production branch for ICM in the APAC region|**Deprecated. Indexes are managed in SHC_APAC branch.**
ICM_APAC_AZURE|Production branch for ICM in the APAC Azure region|**Deprecated. Indexes are managed in SHC_APAC branch.**
ICM_APAC_DEV_AZURE|Development branch for ICM in the APAC Azure region|**Deprecated. Indexes are managed in SHC_APAC_DEV branch.**
ICM_APAC_AWS|Production branch for ICM in the APAC AWS region|**Deprecated. Indexes are managed in SHC_APAC branch.**
ICM_APAC_DEV_AWS|Development branch for ICM in the APAC AWS region| **Deprecated. Indexes are managed in SHC_APAC_DEV branch.**

Repo: ICM_Backup
Backs up: /opt/splunk/etc every hour.
 

**Branch** | Description| **Notes**
---|-----|------
ICM_AMER_usatramekj039|Production branch backup for the AMER ICM|
ICM_AMER_RDC_am1436l051|Production branch backup for the AMER RDC|
ICM_AMER_AZURE_az1436l001|Production branch backup for the AMER Azure ICM|
ICM_AMER_AWS_aw1436l001|Production branch backup for the AMER AWS ICM|
ICM_EMEA_eu1436l015|Production branch backup for the EMEA ICM|**Deprecated.**
ICM_EMEA_AZURE_az1436l012|Production branch backup for the EMEA Azure ICM|**Deprecated.**
ICM_EMEA_AWS_aw1436l018|Production branch backup for the EMEA AWS ICM|**Deprecated.**
ICM_APAC_ap1436l015|Production branch backup for the APAC ICM|**Deprecated.**
ICM_APAC_AWS_aw1436l031|Production branch backup for the APAC Azure ICM|**Deprecated.**
ICM_APAC_AZURE_az1436l020|Production branch backup for the APAC AWS ICM|**Deprecated.**


---

**Deployment Server**
---
Repo: DS_Backup
Backs up: /opt/splunk/etc every 5th minute on a hourly basis.

**Branch** | Description| **Notes**
---|-----|------
DS_AMER_usatramekj043|Production branch backup for the AMER DS|
DS_AMER_AZURE_az1436l002|Production branch backup for the AMER Azure DS|
DS_AMER_AWS_aw1436l002|Production branch backup for the AMER AWS DS|
DS_EMEA_eu1436l032|Production branch backup for the EMEA DS|
DS_EMEA_AZURE_az1436l013|Production branch backup for the EMEA Azure DS|
DS_EMEA_AWS_aw1436l019|Production branch backup for the EMEA AWS DS|
DS_APAC_ap1436l032|Production branch backup for the APAC DS|
DS_APAC_AZURE_az1436l021|Production branch backup for the APAC Azure DS|
DS_APAC_AWS_aw1436l032|Production branch backup for the APAC AWS DS|

---

**DMC Server**
---
Repo: DMC
Deploys to /opt/splunk/etc/apps
 
**Branch** | Description| **Notes**
---|-----|------
DMC_AMER|Production branch for the AMER DMC|
DMC_EMEA|Production branch for the EMEA DMC|**Deprecated. Apps merged to SHC_EMEA branch.**
DMC_APAC|Production branch for the APAC DMC|**Deprecated. Apps merged to SHC_APAC branch.**
---

**Heavy Forwarders (On-Prem)**
---
Repo: HF
Backs up: /opt/splunk/etc/apps every hour.
 
**Branch** | Description| **Notes**
---|-----|------
HF_AMER_usatramekj030|Production branch backup for usatramekj030|
HF_AMER_usatramekj031|Production branch backup for usatramekj031|
HF_AMER_usatramekj032|Production branch backup for usatramekj032|
HF_AMER_usatramekj033|Production branch backup for usatramekj033|
HF_AMER_usatramekj130|Production branch backup for usatramekj130|
HF_AMER_usatramekj131|Production branch backup for usatramekj131|
HF_AMER_usatramekj132|Production branch backup for usatramekj132|
HF_AMER_usatramekj133|Production branch backup for usatramekj133|
HF_AMER_CANATLSIS01|Production branch backup for CANATLSIS01|
HF_AMER_CANATLSIS02|Production branch backup for CANATLSIS02|
HF_AMER_CANATLSIS03|Production branch backup for CANATLSIS03|
HF_AMER_CANATLSISR01|Production branch backup for CANATLSISR01|
HF_AMER_CANATLSISR02|Production branch backup for CANATLSISR02|
HF_AMER_CANATLSISR03|Production branch backup for CANATLSISR03|
HF_US_ushdc8887n01|Production branch backup for ushdc8887n01|
HF_US_ushdc8887n02|Production branch backup for ushdc8887n02|
HF_US_ushdc8887n03|Production branch backup for ushdc8887n03|
HF_EMEA_EU1436L037|Production branch backup for EU1436L037|
HF_EMEA_EU1436L038|Production branch backup for EU1436L038|
HF_EMEA_EU1436L039|Production branch backup for EU1436L039|
HF_EMEA_EU1436L040|Production branch backup for EU1436L040|
HF_EMEA_EU1436L073|Production branch backup for EU1436L073|
HF_EMEA_EU1436L074|Production branch backup for EU1436L074|
HF_EMEA_EU1436L075|Production branch backup for EU1436L075|
HF_EMEA_EU1436L076|Production branch backup for EU1436L076|
HF_APAC_AP1436L037|Production branch backup for AP1436L037|
HF_APAC_AP1436L038|Production branch backup for AP1436L038|
HF_APAC_AP1436L039|Production branch backup for AP1436L039|
HF_APAC_AP1436L040|Production branch backup for AP1436L040|
HF_APAC_AP1436L073|Production branch backup for AP1436L073|
HF_APAC_AP1436L074|Production branch backup for AP1436L074|
HF_APAC_AP1436L075|Production branch backup for AP1436L075|
HF_APAC_AP1436L076|Production branch backup for AP1436L076|


---

**Heavy Forwarders (Cloud)**
---
Repo: HF_Cloud
Backs up: /opt/splunk/etc/apps every hour.

**Branch** | Description| **Notes**
---|-----|------
HF_AMER_AZURE_az1436l003|Production branch backup for az1436l003|
HF_AMER_AZURE_az1436l004|Production branch backup for az1436l004|
HF_AMER_AZURE_az1436l005|Production branch backup for az1436l005|
HF_AMER_AZURE_az1436l006|Production branch backup for az1436l006|
HF_AMER_AZURE_az1436l007|Production branch backup for az1436l007|
HF_AMER_AZURE_az1436l008|Production branch backup for az1436l008|
HF_AMER_AWS_aw1436l003|Production branch backup for aw1436l003|
HF_AMER_AWS_aw1436l004|Production branch backup for aw1436l004|
HF_AMER_AWS_aw1436l005|Production branch backup for aw1436l005|
HF_AMER_AWS_aw1436l006|Production branch backup for aw1436l006|
HF_AMER_AWS_aw1436l007|Production branch backup for aw1436l007|
HF_AMER_AWS_aw1436l008|Production branch backup for aw1436l008|
HF_AMER_AWS_aw1436l009|Production branch backup for aw1436l009|
HF_AMER_AWS_aw1436l010|Production branch backup for aw1436l010|
HF_AMER_AWS_aw1436l011|Production branch backup for aw1436l011|
HF_EMEA_AZURE_az1436l014|Production branch backup for az1436l014|
HF_EMEA_AZURE_az1436l015|Production branch backup for az1436l015|
HF_EMEA_AZURE_az1436l016|Production branch backup for az1436l016|
HF_EMEA_AZURE_az1436l034|Production branch backup for az1436l034|
HF_EMEA_AZURE_az1436l035|Production branch backup for az1436l035|
HF_EMEA_AZURE_az1436l036|Production branch backup for az1436l036|
HF_EMEA_AWS_aw1436l020|Production branch backup for aw1436l020|
HF_EMEA_AWS_aw1436l021|Production branch backup for aw1436l021|
HF_EMEA_AWS_aw1436l022|Production branch backup for aw1436l022|
HF_EMEA_AWS_aw1436l023|Production branch backup for aw1436l023|
HF_EMEA_AWS_aw1436l024|Production branch backup for aw1436l024|
HF_EMEA_AWS_aw1436l025|Production branch backup for aw1436l025|
HF_APAC_AZURE_az1436l022|Production branch backup for az1436l022|
HF_APAC_AZURE_az1436l023|Production branch backup for az1436l023|
HF_APAC_AZURE_az1436l024|Production branch backup for az1436l024|
HF_APAC_AZURE_az1436l049|Production branch backup for az1436l049|
HF_APAC_AZURE_az1436l050|Production branch backup for az1436l050|
HF_APAC_AZURE_az1436l051|Production branch backup for az1436l051|
HF_APAC_AWS_aw1436l033|Production branch backup for aw1436l033|
HF_APAC_AWS_aw1436l034|Production branch backup for aw1436l034|
HF_APAC_AWS_aw1436l035|Production branch backup for aw1436l035|
HF_APAC_AWS_aw1436l036|Production branch backup for aw1436l036|
HF_APAC_AWS_aw1436l037|Production branch backup for aw1436l037|
HF_APAC_AWS_aw1436l038|Production branch backup for aw1436l038|



---

**Universal Forwarders**
---
Repo: UF
Backs up: /opt/splunkforwarder/etc/apps every hour.
 
**Branch** | Description| **Notes**
---|-----|------
UF_AMER_usatramekj037|Production branch backup for usatramekj037|
UF_AMER_usatramekj038|Production branch backup for usatramekj038|
UF_AMER_usatramekj046|Production branch backup for usatramekj046|
UF_AMER_usatramekj136|Production branch backup for usatramekj136|
UF_AMER_usatramekj137|Production branch backup for usatramekj137|
UF_AMER_usatramekj160|Production branch backup for usatramekj160|
UF_AMER_usatramekj161|Production branch backup for usatramekj161|
UF_AMER_usatramekj179|Production branch backup for usatramekj179|
UF_AMER_usatramekj180|Production branch backup for usatramekj180|
UF_AMER_usatramekj212|Test branch backup for usatramekj212|
UF_US_ushdc8887n01|Production branch backup for ushdc8887n01|
UF_US_ushdc8887n02|Production branch backup for ushdc8887n02|
UF_US_ushdc8887n0|Production branch backup for ushdc8887n03|
UF_US_ushdc8887n04|Production branch backup for ushdc8887n04|
UF_US_ushdc8887n05|Production branch backup for ushdc8887n05|
UF_US_ushdc8887n13|Production branch backup for ushdc8887n13|
UF_US_ushdc8887n14|Production branch backup for ushdc8887n14|
UF_US_usndc8887n15|Production branch backup for usndc8887n15|
UF_APAC_AP1436L041|Production branch backup for AP1436L041|
UF_APAC_AP1436L042|Production branch backup for AP1436L042|
UF_APAC_AP1436L043|Production branch backup for AP1436L043|
UF_APAC_AP1436L044|Production branch backup for AP1436L044|
UF_APAC_AP1436L077|Production branch backup for AP1436L077|
UF_APAC_AP1436L078|Production branch backup for AP1436L078|
UF_APAC_AP1436L079|Production branch backup for AP1436L079|
UF_APAC_AP1436L080|Production branch backup for AP1436L080|
UF_EMEA_EU1436L041|Production branch backup for EU1436L041|
UF_EMEA_EU1436L042|Production branch backup for EU1436L042|
UF_EMEA_EU1436L043|Production branch backup for EU1436L043|
UF_EMEA_EU1436L044|Production branch backup for EU1436L044|
UF_EMEA_EU1436L077|Production branch backup for EU1436L077|
UF_EMEA_EU1436L078|Production branch backup for EU1436L078|
UF_EMEA_EU1436L079|Production branch backup for EU1436L079|
UF_EMEA_EU1436L080|Production branch backup for EU1436L080|

---

**Search Heads**
---
Repo: SH
Backs up: /opt/splunk/etc every hour.

**Branch** | Description| **Notes**
---|-----|------|
SH_AMER_usatramekj001|Production branch backup for usatramekj001||
SH_AMER_usatramekj002|Production branch backup for usatramekj002||
SH_AMER_usatramekj003|Production branch backup for usatramekj003||
SH_AMER_usatramekj100|Production branch backup for usatramekj100||
SH_AMER_usatramekj101|Production branch backup for usatramekj101||
SH_APAC_ap1436l012|Production branch backup for ap1436l012|**Deprecated.**|
SH_APAC_ap1436l013|Production branch backup for ap1436l013|**Deprecated.**|
SH_APAC_ap1436l014|Production branch backup for ap1436l014|**Deprecated.**|
SH_APAC_ap1436l069|Production branch backup for ap1436l069|**Deprecated.**|
SH_APAC_ap1436l070|Production branch backup for ap1436l070|**Deprecated.**|
SH_EMEA_AZURE_az1436l056|Production branch backup for az1436l056|**Deprecated.**|
SH_EMEA_AZURE_az1436l057|Production branch backup for az1436l057|**Deprecated.**|
SH_EMEA_AZURE_az1436l058|Production branch backup for az1436l058|**Deprecated.**|
SH_EMEA_AZURE_az1436l059|Production branch backup for az1436l059|**Deprecated.**|
SH_EMEA_AZURE_az1436l060|Production branch backup for az1436l060|**Deprecated.**|
SH_EMEA_AZURE_az1436l061|Production branch backup for az1436l061|**Deprecated.**|
SH_EMEA_AZURE_az1436l062|Production branch backup for az1436l062|**Deprecated.**|
SH_EMEA_AZURE_az1436l063|Production branch backup for az1436l063|**Deprecated.**|
SH_EMEA_AZURE_az1436l064|Production branch backup for az1436l064|**Deprecated.**|
SH_EMEA_AZURE_az1436l065|Production branch backup for az1436l065|**Deprecated.**|
SH_EMEA_AZURE_az1436l066|Production branch backup for az1436l066|**Deprecated.**|
SH_EMEA_AZURE_az1436l068|Staging branch backup for az1436l068|**Deprecated.**|
