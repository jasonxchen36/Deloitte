The following entry describes briefly the build-pipeline.yml checks performed whenever a PR gets created. This checks are performed when the project pipeline runs and makes sure that the configuration that is going to be pushed follows our guidelines and standards.

These are the checks performed by the script:

1 - Verify metadata

Checks if the metadata files uploaded in the PR (default.meta and local.meta) meet the standards proposed in the wiki:
https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/28/Known-default.meta-Files

2 - Verify Indexes are in correct app and format
This include the following checks:


- Paths (homePat, coldPath, tstatsHomePath, thawedPath), maxHotSpanSecs, maxHotIdleSecs and frozenTimePeriodInSecs correctly configured.
- Index naming follows guidelines.
- Index created in allowed app, not all apps are meant to have indexes.conf.



