The following entry describes briefly the build-pipeline.yml checks performed whenever a PR gets created. This checks are performed when the project pipeline runs and makes sure that the configuration that is going to be pushed follows our guidelines and standards.

These are the checks performed by the script:

1 - Verify that changes were tested in staging.
First it checks if the changes you are applying to prod environment where previously tested and pushed to Staging environment.

2 - Verify metadata.
Checks if the metadata files uploaded in the PR (default.meta and local.meta) meet the standards proposed in the wiki:
https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/28/Known-default.meta-Files

3 - Find whitespaces after new line indicator.
Checks for whitespaces that might affect the configuration after new lines.

4 - Verify searches are added disabled and unsummarized.
Checks that the searches uploaded (savedsearches.conf) have the following stanzas included:

disabled = 1
realtime_schedule = 0

This is because we enable the searches afterwards on the GUI.

5 - Verify content labels are not too long.
Checks for saved searches longer than 100 characters. Splunk does not allow to enable searches name that long.

6 - Flag changes to rename commands.
Checks for rename commands

7 - Disallow Uploading Custom Lookups.
Checks for lookups uploaded via git (backend). The way we upload lookups is using the GUI.

8 - Check for Modification of Protected Applications.
Checks for any modification performed on the apps that belong to the protected apps list, this is because certain apps need to be as they come from Splunkbase or are special apps provided by Splunk.

9 - Disallow SNOW tickets in Volume Testing.
Check for the stanzas responsible for ticket creation for saved searches uploaded to the DEV content app.

10 - Check for New Applications without local.meta clearing and branch syncing.
Checks if a newly added app has been included in the lists accordingly for branch syncing and loca.meta clearing (since the metadata file we need to use is the default one).
For more info about branch syncing please see:
https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/745/Synchronization-Process-Across-Regions


11 - Do not complete PRs within 24 hours of a push.
Do not complete PRs in a short time window before a push.

