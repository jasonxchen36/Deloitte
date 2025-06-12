For lookups that support production content: 
1. Determine if lookup is static or dynamically populated

2. If the lookup is static, add the lookup via the Splunk web gui on a production ES Search Head
   - When adding a lookup via the gui, please make sure you specify App Context: If it's a global lookup then add it to the app **DA-ESS-Global-Lookups**  or if it's a regional lookup then add it to the region specific lookup app (i.e. **DA-ESS-Americas-Lookups**, **DA-ESS-EMEA-Lookups**,**DA-ESS-APAC-Lookups**)
   -  Please make sure to create a lookup definition for each lookup (also specify app context for this)

3. If a lookup is dynamic (has a savedsearch populating it), the savedsearch config needs to be added to the specific lookup app (For global lookup, add to the app **DA-ESS-Global-Lookups** and for regional lookups, add to the region specific lookup app) in Devops and pushed from the deployer.
   - The initial csv file (if one exists) should still be added to the web gui in the correct App Context
   - A lookup definition should be defined via the web gui in the correct app context



**Note***: For our FC content filter lookups, please maintain a “-“ under “comment” column as one minimum row. This is to avoid FPs which have been triggered via “SPM - Missing Lookup Value (Region)” alert detecting 0 entries from the lookup.