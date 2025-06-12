Here steps to login into GCP console

1.  Login to [https://uspcs/USPCS/app/#/secret/72367/general](https://uspcs/USPCS/app/#/secret/72367/general "https://uspcs/uspcs/app/#/secret/72367/general") and get the [us.deloitte.com\es-account@deloitte.com](mailto:usa-account@deloitte.com "mailto:usa-account@deloitte.com") creds.

2.  Login as incognito browser 

3.  Open GCP ULR [https://console.cloud.google.com/](https://console.cloud.google.com/ "https://console.cloud.google.com/") link

![image.png](/.attachments/image-4661bba7-fc14-45e1-ab66-d94e1748b404.png)

![image.png](/.attachments/image-02888e4c-115a-4c0d-8d0a-a9b36bbd72b8.png)


4.  Select resource **DELOITTE.COM**  
        ![clip_image002.png](/.attachments/clip_image002-d8443b21-d96c-4931-b620-32e28fad00a1.png)
**5.**     Select project **us-gcp-ame-its-splunk-prd-1**
![clip_image004.png](/.attachments/clip_image004-4289137e-e363-453f-93f0-c4365e6e1ca2.png) 
6. Click navigation menu, then click Compute Engine --> Virtual machines --> VM instances
7. then click on SSH to launch the CLI of the server or copy the IP and login from putty application using us.deloitte.com\es-account@deloitte.com creds.
![clip_image006.png](/.attachments/clip_image006-9d31aabd-e5f3-4f6c-97f1-180cc078cb5a.png)
**Service account** is sudo su - splunk
**servers**:

| usgcpenam0540<br> | 10.218.3.67<br> | CyberSec Prod Splunk Deployment Server GCP<br> | GCP<br> |
| --- | --- | --- | --- |
| usgcpenam0541<br> | 10.218.3.81<br> | CyberSec Prod Splunk Heavy Forwarder GCP (GCP Pull)<br> | GCP<br> |
| usgcpenam0542<br> | 10.218.3.84<br> | CyberSec Prod Splunk Heavy Forwarder GCP (GCP UF Listen)<br> | GCP<br> |
| [taps-server-1](https://console.cloud.google.com/compute/instancesDetail/zones/us-east4-c/instances/taps-server-1?inv=1&invt=AbxRoA&project=us-gcp-ame-its-dcs-splunk)<br> | 10.218.3.76<br> | Prod UF<br> | GCP<br> |
| [usgcpenam0515](https://console.cloud.google.com/compute/instancesDetail/zones/us-east4-c/instances/usgcpenam0515?inv=1&invt=AbxRoA&project=us-gcp-ame-its-dcs-splunk)<br> | 10.218.3.70<br> | DEV<br> | GCP<br> |