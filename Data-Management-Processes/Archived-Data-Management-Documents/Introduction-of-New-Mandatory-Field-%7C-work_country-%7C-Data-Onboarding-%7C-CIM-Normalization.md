Introduction of a new mandatory field "**work_country**" for all data onboarding efforts

• Create 1 index per region, example amer_cloud_netskope_casb for AMER region and onboard the logs from the MFs (US, MX, CA) belonging to the same region

• In order to search for the Netskope logs in the above example the search filter would be index= amer_cloud_netskope_casb **work_country**=US

**Points to remember while Data Onboarding:**

• Some of the log sources are using field name as "member_firm" today and others are using field name as "work_country". We need to have a standard field going forward. These are usually countries and not MFs, so **work_country** will be more appropriate.

• This does not apply to log sources that are ingested from a Member Firm/Country data center. Those log source should remain in the specific indexes

• Applying this field should be the norm and if this field can’t be determined, we need a very good reason why and document the exception

• This field should be added as a meta data field and not included in raw. That way we do not increase our license usage. However, this may become less important as we migrate to Splunk Cloud. 

• It would be pertinent to include the work_country field name for the indexes having the MF or the country name in it. While it would be duplicative due to the index name, it would allow for flexibility in the future.