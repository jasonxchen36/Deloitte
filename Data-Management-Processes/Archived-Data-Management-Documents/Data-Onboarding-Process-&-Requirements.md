Steps Taken
##Development
- Establish Firewall Connectivity 
- Validate logs are coming into Splunk
- Validate all logs can be seen coming into Splunk
- Add timestamp configurations
- Review data for private information https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/375/Full-or-Partial-Name-Masking-Information 
- Review Data Source With Content Team
- Update Props
- Update transforms
- Update Tags
- Update eventtypes
- Update Data Model Macro (Make sure that the macros.conf for the DM is updated to include the new index so those logs flow into the DM)
- Verify with content team

###Stage
- Test Changes on Standalone
- Confirm changes made in data model pivot
- Test Changes in stage search head cluster
- Verify with content team

##Production
- Test Changes in Production Search Head cluster
- Verify with content team
- Create or update documentation


** Log sources are limited to production systems