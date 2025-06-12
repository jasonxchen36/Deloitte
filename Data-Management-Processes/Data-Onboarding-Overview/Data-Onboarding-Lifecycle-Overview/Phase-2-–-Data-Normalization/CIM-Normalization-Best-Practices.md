##Splunk CIM Data Model Documentation
https://docs.splunk.com/Documentation/CIM/4.14.0/User/Overview 

##Gotchyas
- macros.conf (if a new index)
-- During Ready for Stage Test and Ready for Production states, make sure to add the index for the new data to the macros.conf in Splunk_SA_CIM app, without this the data will not populate the data model
 
- Using field alias vs calculated field in props.conf
-- Sometimes using field alias doesn't always work during search time, recommended approach is to use a calculated field (EVAL on the backend)
-- If Engineer still wants to use field alias, please make sure to test that field alias is working appropriately

- Make changes to CIM as granular as possible
-- While making changes within a data source, make sure that the changes you make are as granular as possible, e.g., if src_user needs to be mapped to ID in Windows data where EventCode is 4624 - use an if statement where EventCode=4624 instead of making the mapping global against the source type

- Make sure that change will not affect existing content
-- Usually only a problem on changes to the entire sourcetype - please make sure to check with Global FC Engineering Content team if change is to an entire sourcetype


##Best Practices
- Test all mappings on standalone SH
- Follow the processes laid out in CIM Normalization Boards Processes wiki
- Use eventtypes.conf to define searches that your tags and mappings will apply to
- Use tags.conf to define any tags used - tags are important as they are required for data to be fed into DM
- Use props.conf to map fields - suggest using EVAL fields but can also use FIELDALIAS if Engineer verifies FIELDALIAS is working appropriately
- Use macros.conf to add new indexes to the appropriate DM macro - data will not feed to DM if this step isn't performed
- Leverage Splunk CIM DM documentation (referenced above) to make sure all tags are present for DM and the fields are correctly mapped
- During Stage Test and Ready for Prod Verification states, make sure to test new mappings in DM pivot table and results are accurate/expected
- During Stage Test and Ready for Prod Verification states, make sure to test the Test Search String field in the CIM Validation Request Work Item and results are accurate/expected
