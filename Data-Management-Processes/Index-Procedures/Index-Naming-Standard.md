**Why revisit our index naming convention?**

1. To reduce the impact of searching when we migrate to Splunk Cloud
1. To create a more unified approach for our index naming convention
1. To provide better visibility for stakeholders on what data is in each index


**Old Naming Convention**
![image.png](/.attachments/image-1304e6d3-8179-49bc-95be-19036b67d18a.png)

_example of old naming convention: uk_endpoint_microsoft_windows_security_ 


The current index naming convention incentivizes usage of preceding wildcards to match vendor or technology across multiple member firms in a given region. This drastically increases search time as Splunk attempts to match the leading wild card to each character of the entire index range until a direct match, in most cases the first underscore, is located. Reversing the naming convention and standardizing it to four sections will reduce the number of searches utilizing a preceding wild card which will improve overall search performance and reduce SVC utilization in Splunk Cloud. The feedback and new approach has been validated by Splunk PS.

**New Naming Convention**
![image.png](/.attachments/image-368cd9cc-32a0-45bc-82c8-b9026c8bbae0.png)

**_Please note the naming convention structure can only contain four (4) sections as show in the image above._**

_example of new naming convention:_ endpoint_microsoft_security_uk 

**_Endpoint:_** The logical group of data sources based on the types of logs contained. The intent is to have a small, set list of categories that users can easily navigate. Data models cannot be used for this category because of the number of indexes that are applicable to multiple data models. 

**_Vendor/App_**: The name of the vendor or application name providing data to the index. It is expected that the choices for this identifier will be updated on a regular basis. Based on net new data sources.

**_Function:_** The additional description to find logs contained in the index. While this field may have many choices, the goal will be to keep the choices consistent.  

_**[Member Firm/Region:](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/463/Member-Firm-Country-Codes)**_ Member Firm (MF), Geography, Region, may also include appended MF specific deployments (i.e. ustax, amerdisconnected, etc.).

**_Standard Categories_**
Below is a list of standard categories currently in Splunk:

1. application
1. authentication
1. email
1. encryption
1. endpoint
1. internal
1. network
1. platform
1. referential
















