In the process to move Checkpoint to Cloud in SAAS solution manage by vendor, it is necessary to create new flow and configurations by MF and sources.

This new infrastructure manage by Checkpoint Vendor is hosting in AWS, for this reason, we need to ingest in AWS infrastructure.

Here is a overview of flow:

Data source > Public LB > (AMER-PUBHEC-LB) > IP Forwarders > Endpoint > Data LB > (Main Security Group) > Target HF

1. First step is request a new certificate to install into our AWS LB. This certificate need to create by MF in Checkpoint SAAS platform, and then we need to upload in AWS Certificate Manager:

![image.png](/.attachments/image-fbb1efcf-88d6-4b34-a018-a045023d14bb.png)

2. The certificate name need to be the same of the AWS LB DNS Name

![image.png](/.attachments/image-6d9a5669-721c-4cb2-8ef3-6e0d9eb3de2e.png)

3.We need to define/create a new listener group with **Protocol TLS and using the certificate**

![image.png](/.attachments/image-1d6ff4da-3e80-4ce8-ae27-16ba9f9d34ea.png)

![image.png](/.attachments/image-f666b46d-f3e7-4e4e-9e0f-a59670f8d31c.png)
![image.png](/.attachments/image-4a27cd8a-9ed1-4f36-994d-392e1205473f.png)

![image.png](/.attachments/image-3773b0c6-f087-405e-a2b8-b63e8dd90813.png)

4. Open ports in Security Group assocaite weith the AWS LB

![image.png](/.attachments/image-114f2b77-952d-48c0-af38-a14ca24e22b2.png)

![image.png](/.attachments/image-658605bf-c7e3-4023-b79e-068c75548fd8.png)

5. Now enables the ports and source Ip in the Disconnected machines. [Here](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/791/AWS-Disconnected-IP-Forwarders-Configurations) some examples


With this setup we send all events over internet to our Public AWS LB and forwarded to an IP Forwarding machines, these machines forward to an internal AWS LB, and finally stored the events into internal syslogserver.
Now lets go with the final setup

6. In our internal AWS LB we need to add/create a listener group with ober protocol and port

![image.png](/.attachments/image-57b2c386-a57b-4e90-aa74-3a21fe0319a7.png)

![image.png](/.attachments/image-fd8b86ff-cadd-4ec3-a7ea-828ce61b6ef2.png)

7. FInally we need to setup syslogserver with the correct certificate and inputs.conf

![image.png](/.attachments/image-3c1df774-56ea-47e8-aef3-57a867dd63c6.png)
![image.png](/.attachments/image-5dc240e1-176d-4b25-8e9f-10b08ecf3acf.png)

![image.png](/.attachments/image-6b869e27-bde7-47f3-8b48-5b6b94404e4d.png)

**Troubleshooting**

Checkpoint can update the source IPs from their end, and can change, in that case we will stop to get events, because we are filtering in LB using Security Gropus and Network ACL filters, so we need to update.
To be sure which are the new IPs, we need to contact with **Reynders, Timothea** <treynders@deloitte.ca> and **CA Networks** <CANationalNetworks@deloitte.ca>

Here there is other KB article from CP, where we can try to track the sources IPs

[sk182699 - Changes to Smart-1 Cloud external/outbound IP addresses and domain names](https://support.checkpoint.com/results/sk/sk182699)

Now, the list of allowed Sources IPs is:
  
- 18.205.54.240
- 50.17.39.153
- 3.224.33.252

We can validate is the traffic is coming across our LB with the following query:

Working fine

![image.png](/.attachments/image-b3ad4081-f9bc-4aa5-b9da-c520c8e17546.png)

Not working

![image.png](/.attachments/image-9458477a-9e2c-4b0b-a904-03a670324af7.png)

In case any problem with the log format, we can review with Canada team about the syslog format in their end, Splunk format is the correct one

![image.png](/.attachments/image-159aeabe-6c90-4e41-8d20-a6c91936a99a.png)









