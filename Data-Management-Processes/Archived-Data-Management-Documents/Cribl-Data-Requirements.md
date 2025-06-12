This page summarizes the various data requirements for onboarding data through Cribl.

## **"user_work_country" field**

The field is used to describe either:
1) work_country - based on email address found in "deloitte_ldap_identities.csv" lookup
2) member_firm - based on the member_firm that can be identified from various UIDs in the events or the index name

------
work_country:
 -  Lookup is found on Prod ES Splunk Search Head Cluster (SHC) in all regions. 
| inputlookup deloitte_ldap_identities.csv | fields email, work_country | dedup email
 -  Splunk lookup is manually added as a lookup called "deloitte_ldap_identities_reduced.csv" to Cribl Worker Groups on a monthly basis.
![image.png](/.attachments/image-cd0fe58a-5584-4e59-9a46-400d16b8793f.png)
- Cribl uses "deloitte_ldap_identities_reduced.csv" lookup with email address as the input to define "user_work_country" field as the output
![image.png](/.attachments/image-76475e0d-b92e-43e6-a32b-0adedbbaa3b4.png)
- Cribl uses "workcountry_index_prefix.csv" lookup to normalize the value of the "user_work_county" field (Example changing "UNITED KINGDOM" to "United Kingdom").
![image.png](/.attachments/image-70398814-ca82-459a-a08c-ef7a6559ac82.png)
- Add "user_work_country" as an index/metadata field in Cribl


## **Indexes**
Splitting data by region based indexes ("amer", "emea" and "apac"):
   - The field "user_work_country" is the identifier to determine which region the data should be sent to 
(E.g. user_work_country="United States" means data will go to "amer" index")

   - Using the "all" index for a catch-all basis if we cannot identify the user_work_country. These events will show as user_work_country="Unknown"
