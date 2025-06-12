This process describes how to renew any of the Load Balancer certificates for F5 on Venafi. Each region has 3 certificates, one for Prod, one for QA or Development and one for Staging.
- Prod:
`amersplunk.atrame.deloitte.com (GIS F5)`
`apacsplunk.atrame.deloitte.com (GIS F5)`
`emeasplunk.atrame.deloitte.com (GIS F5)`

- QA:
`amerdsplunk.atrame.deloitte.com (GIS F5)`
`apacdsplunk.atrame.deloitte.com (GIS F5)`
`emeadsplunk.atrame.deloitte.com (GIS F5)`

- Staging:
`amersplunkstage.atrame.deloitte.com (GIS F5)`
`apacsplunkstage.atrame.deloitte.com (GIS F5)`
`emeasplunkstage.atrame.deloitte.com (GIS F5)`

## Certificate Renewal.

In order to renew any of the certificates we need to access Venafi and have the SSL certificate for the SH also renewed.

First of all, we need to access the settings tab. Then in order to renew the certificate change the **Management Type** from Provisioning to Enrollment, and click **Save**.

![image.png](/.attachments/image-edd0ffb0-8729-4e76-af74-c32eb146b0e7.png)

**NOTE:** If encounter an error regarding Install Type while saving set it to Partially Automated

Once this configuration is saved. 

We can renew the certificate clicking on **Renew now**.

Finally, after renewal we will need to set the **Management Type** again to Provisioning and saving.

## App Renewal.

In order to push the apps go to the **Summary** tab and push every single app listed.

![image.png](/.attachments/image-c6df8041-e86c-4b57-978a-4214d1bee805.png)

Then we will **Push** the app, wait for the **Status** to be set to **OK** and make sure the Certificate and Key File value contains the new expiration date. Finally click Save.

![image.png](/.attachments/image-e7cf9d8e-9b53-4520-981c-d9f635aa5824.png)
