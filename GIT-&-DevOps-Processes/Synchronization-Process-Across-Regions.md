The following wiki guide us through the replication of files and configurations across the different environments. 

**_First of all, this only applies to the SHC repository and to Production environment._**

The process consists in replicating the applications and configurations from the AMER PROD branch into the rest of regions. The list that contains all the applications or paths that get replicated can be found below:

https://dev.azure.com/GlobalSOC/Splunk/_git/SHC?path=/Automation-Scripts/sync-config/synced_applications.txt&version=GBSHC_AMER&_a=contents

Also, inside this routes there are certain specific paths that we exclude for different reasons (for example, region-specific content):

https://dev.azure.com/GlobalSOC/Splunk/_git/SHC?path=/Automation-Scripts/sync-config/unsynced_paths.txt&version=GBSHC_AMER&_a=contents

Currently, we have three different pipelines configured in this project, one of them being the synchronization one:

![image.png](/.attachments/image-9dc8e60c-a419-43cf-8f13-e204351182b7.png)

Every time a PR gets approved and completed in SHC_AMER the pipeline runs and checks if the files edited in the PR are in the sync list, if they are then a PR gets created with the changes. The created PR has the following naming:

**Sync changes from SHC_AMER into the SHC_<REGION> branch**

The newly created PR will be reviewed and approved and then pushed.

Also, there is another process that consists in building the Global SHs from the current region specific one. The process follows the same steps as the one explained above but instead of copying from AMER to the other regions, it copies from every region into the global SHC: SHC_EMEA_AZURE. 

The lists containing the synced and not synced paths can be found here:

![image.png](/.attachments/image-d3efee9d-5c13-4715-861f-07251f5d4519.png)

This will sync from the specific region into the global one. Any app that needs to be replicated needs to be added into above lists in SHC_AMER branch (even if the app is from EMEA or APAC environment) because the pipeline gets the information from AMER branch.