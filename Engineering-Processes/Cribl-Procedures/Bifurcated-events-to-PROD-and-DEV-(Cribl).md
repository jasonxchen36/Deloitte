
In some cases is necessary to ingest events in production and development at same time. For this porpoise we develop an Outputs route, to send event over Cribl at same time, and works in fields extraction or whatever we need.
It is very important to validate that we have the index in or other index setting in Splunk DEV

We need setup our Output with the route

![image.png](/.attachments/image-27d89bb7-7ac5-49c5-a9ad-a9737470d772.png)

Later, we need to setup the outputs with the filter and Splunk environment (Prod and Dev)
We need to add whatever we need

![image.png](/.attachments/image-34d3ca69-8a5b-48c7-8b99-6127596e52e9.png)


![image.png](/.attachments/image-6d1cb73a-d3f2-440a-9087-697fb72c1dc8.png)

**NOTE**: Keep in mind is very import to commit and deploy the changes

## **Troubleshooting**

Some point to review in case issue:

### Certificates

![image.png](/.attachments/image-d9756704-5871-4e04-bd5b-78fe5d16baa4.png)

![image.png](/.attachments/image-ba3dd99e-a9c2-4308-aa00-35c66e6189ca.png)

### Load Balanced:

![image.png](/.attachments/image-783e683e-0cb5-4fa6-b397-9fd46458ef19.png)





