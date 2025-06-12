The User Data Access dashboard is the only acceptable way for user data to be accessed in Splunk. It can be accessed by navigating through the Enterprise Security application and selecting "User Data Access NTK" in the navigation bar under "GEMS Analytic Tools".
Upon opening the dashboard, you will see the following: 

![image.png](/.attachments/image-a64c3a6a-2c99-4439-aab2-c21f67551a98.png)
 
The dashboard has 3 necessary inputs, without which access to user data will not be granted. The first, "Ticket Number," requires input of the ticket ID related to the access request. Both SIR and INC tickets can be used, although since INC ticket data is not currently ingested in Splunk specific details about the ticket owner and ticket title will not be available in the dashboard. The second, "User," is the exact username data is being requested for. Multiple usernames separated by a space can be entered. Last, a justification for the access request must be selected from a dropdown under "Access Justification." After providing these three inputs, click the submit button. Provided the username(s) and ticket are valid, the top panel, "User Data," will become populated with various details about the user, like below:

![image.png](/.attachments/image-83604249-2e57-41f6-9d70-3af25aacc1b1.png)
 
Additionally, a record of the access request will be created:
 
![image.png](/.attachments/image-a09a35e7-b077-487e-884e-efde283f655f.png)

There are a number of data sources and lookup table files underlying the functionality of this dashboard. The first data source, the amer_user_access_category index, pulls Active Directory data for all users. This is the data source that is directly queried for results in the “User Data” panel of the dashboard.

![image.png](/.attachments/image-7dbdd1c7-6dee-4063-8772-3469a680cb7a.png)
 
The second data source, the all_ticketing_servicenow index, is used by both panels to confirm the input SIR ticket number is valid. The second panel also uses this data source to pull data on SIR Ticket Owner and SIR Ticket Title.

![image.png](/.attachments/image-fc5c76d7-7d60-4507-885a-8824b912e542.png)
 
Last, the user_data_access_ntk_audit lookup table file stores records of user data access. Every time the dashboard is executed, new record(s) are appended to this lookup table file. This lookup table is backed up every four hours
 
![image.png](/.attachments/image-ba294a02-29ef-416f-b22e-59b5bcbda758.png)