The team has utilized Cribl to encrypt specific data fields for select log sources in Splunk in order to meet Member Firm regulatory requirements for onboarding. The below indicates the current list of impacted indexes and fields:

****Impacted** Indexes:**
1. NSE Netskope (currently in production): nse_cloud_netskope_casb
2. DCE Netskope (currently in production): dce_cloud_netskope_casb 

**Impacted Fields:**
1. from_user
2. to_user
3. ur_normalized
4. user
5. user_id
6. userkey

The following screenshot depicts how the encrypted data looks in Splunk upon searching:

![2024-12-10 151323.png](/.attachments/2024-12-10%20151323-6672cacc-8e39-47ee-8b52-cd202649a3b6.png)

In order to decrypt this data, select Splunk users with appropriate access can run the "cribldecrypt" command as seen in the following screenshot (usernames have been scrubbed for privacy): 

![Cribl Decrypt Command.png](/.attachments/Cribl%20Decrypt%20Command-367139fa-9429-453e-8ede-918f25fc95b8.png)

There is no impact to utilizing the "cribldecrypt" command when searching data that has not been encrypted, as the search will still run.

We have noticed increased search times when utilizing the "cribldecrypt" command on encrypted data and as a result will notify all stakeholders as new fields or log sources get added into scope to review downstream impacts.