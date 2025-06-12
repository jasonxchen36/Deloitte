#FOR CLOUD (EMEA, APAC)
      
**Before the push the app will undergo some validations. The app MUST pass the validation to be pushed: Not all the apps will be validated, check the file Automation-Cloud/SingularApps.json.**
| **SingularApps** | **Validation** |
| --- | --- |
| At SingularApps marked as **Exclusion** | It will **NOT** be validated<br> |
| At SingularApps marked as **SplunkBase** or **ESS**<br> | **ONLY** the local folder will be validated<br> |
| **Not** at SingularApps| **ALL** the app will be validated<br> |


**The different checks performed by the validation are:**
- Verifies if the **default/app.conf** file is present within the application package.
- Checks that the **install_source_checksum** attribute in app.conf is not manually configured, as Splunk generates it automatically.
- Validates the presence of stanzas such as **[id]**, **[launcher]**, and necessary attributes like id or version in **app.conf**.
- Ensures that the **[package] id** attribute in **app.conf** matches exactly with the application's directory name.
- Checks that if the **app.manifest** file exists, it contains the **[info]** or **[id]** stanzas and that these stanzas match correctly with the information provided in **app.conf**.
- Verifies that there are no files or folders outside the application package or with unexpected permissions.
- Reviews that the correct version is present in XML files: **<version=1.1>.**
- Checks that **limits.conf** is not modified, as resource limits should only be managed by Splunk administrators.
- Detects duplicate stanzas in configuration files such as **savedsearches.conf** or **macros.conf.**
- Examines that the configurations in **alert_actions.conf** are complete, including the verification of required executables for alerts.
- Review’s role configurations in files such as **authorize.conf**, ensuring that roles like **admin** are not included in stanzas that could grant unnecessary permissions.

**Instructions when installing a new App:**

1. Upload via PR the configuration to the repo of the needed REGION.
1. The changes at the PR automatically will undergo a validation (Cloud validation at the pipeline)
- If the validation is correct no more action is needed.
- If it is not correct apply the necessary changes to fix the validation issues.
3. At the push window, the changes will be pushed.

-----------------------------------------------------------------------------------------------------
#FOR ON-PREM (AMER)

## When adding a new app into the SHC, there are some things to take into consideration, both Staging and Prod:

1. App should not have an "inputs.conf" file (unless it is necessary)
2. Metadata should meet the requirements under the wiki: https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/28/Known-default.meta-Files
3. Searches must be disabled and unsummarized:
realtime_schedule = 0
disabled = 1
4. Uploading custom lookups is not permitted, only through the GUI.
5. Changes/Additions must be tested in Staging Environment first.
6. New apps must be added to the following lists (Always leave the bottom line empty):
- Automation-Scripts/global-sh-sync-config/SHC_**REGION**_synced_applications.txt - Always, in order to sync this file to global SHs
- Automation-Scripts/sync-config/synced_applications.txt - If the apps belongs to the 3 environments: AMER, EMEA, APAC. (This lists replicates all the Apps installed in AMER to the other two regions)

7. **ADDITIONAL REQUIREMENTS WHEN PUSHING TO PROD:**
- App should be added to the following lists as well (Always leave the bottom line empty):
Automation-Scripts/local_metadata_clear_app_list.txt
Automation-Scripts/local_savedsearches_clear_app_list.txt (if the app has any savedsearches.conf)

-----------------------------------------------------------------------------------------------------

## Instructions when installing a new App into the environment (Both Staging and Prod):

- Two PRs will be created, and only when the first one is approved and completed the second one will pass the build_pipeline requirements:

## **1st PR: Including the app in the Sync-config apps (both local and global): This will always be done in the AMER branch (Staging or Prod), even if the app is being installed in EMEA/APAC as this lists are only present in AMER branches.**
(Always leave the bottom line empty)
- Automation-Scripts/global-sh-sync-config/SHC_**REGION**_synced_applications.txt (this would depend on where the app is going to be installed: AMER, EMEA or APAC)
 - Automation-Scripts/sync-config/synced_applications.txt

## **2nd PR: Installing the app, adding it to clear lists and whitelists (if it needs to):**
If the push is to Prod environment the app should also be added to the following lists as well (Always leave the bottom line empty):
- Automation-Scripts/local_metadata_clear_app_list.txt
- Automation-Scripts/local_savedsearches_clear_app_list.txt (if the app has any savedsearches.conf)

