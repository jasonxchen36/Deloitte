
## **Adding from Thycotic Access Page:-**
When you go to the share tab on a particular secret, we can search and add username to the list.

![image.png](/.attachments/image-49f2dc23-aefb-4b04-b3ff-8b040f8f9ab3.png)

![image.png](/.attachments/image-29d717e5-cf92-4a59-8db8-b84c0d14fab6.png)


If their name doesn't appear, it most likely means that the user doesn't have Global Thycotic access. If that happens you get them access by having either Bob(Bob, Magnus) or Rob(Robert Sukhwani) add them to the "App1436PAMPSplunkAPIAccountsSecretViewers" group in AD.

[AD Link](https://groups.aps.deloitteresources.com/IdentityManagement/aspx/Groups/AllGroupTypes.aspx?searchtype=a9d9d388-0cb8-4511-96f5-5e3bed420eb6&content=App1436PAMPSplunkAPIAccountsSecretViewers)

Incase if you still can't give them view access to the secret, it means their account is locked in Thycotic. 

Access can be requested by submitting SNOW Request and have the added user removed from **1436 AD group** 

Sample Request for Reference: **RITM0718263**  

