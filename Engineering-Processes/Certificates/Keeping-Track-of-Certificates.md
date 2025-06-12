Certificates

Every Monday we have to check the certificates that are close to expire with either the excel or searching in splunk for the index=internal_splunk_prod_[region]. We have a meeting set as: "!!! Weekly Certificate Renewal Review Reminder" as a reminder to do it. This reminder is set by Antonio Rebato.

Alongside the meeting mention above we receive an excel with the certificates with 30, 60 and 90 Day Expiration for our project. "SSL Certificate 60-Day Expiration & 30-Day Violations Report - Week of *". In this excel we should find in each sheet our project: App1436 and check the current state of expiration. For example:
Search:
`index=internal_splunk_prod_amer`
![image.png](/.attachments/image-8ae2b510-a44f-4353-9442-7eaaa975f059.png)

The excel given by Venafi:
![image.png](/.attachments/image-3d599027-0056-44ed-b38b-fd60fb394104.png)

When a certificate is about to expire we receive an email 90, 60, 45 and 30 days before it expires.
Email subject: NOTICE: Expiring Certificate - *Certificate name*
From: dttlctocertificatemanagementservices@deloitte.com

**We must renew certificates before 30 days.**

![image.png](/.attachments/image-05355653-0f07-4055-a47a-568e312f74cd.png)

Then there are other certificates that do not have the same type of notification.
This other certificate is related with Azure and SAML.

Azure certificates are realated with SAML and we get the notification via email also.
Subject: RE: [EXT] Action required: Renew your application certificate in Microsoft Entra ID.
![image.png](/.attachments/image-d02e5cee-f5d2-4c09-b011-6260daf6ecad.png)
Other good practice to check this would be accesing the Azure platform:
[Enterprise applications - Microsoft Azure](https://portal.azure.com/#view/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/~/AppAppsPreview/menuId~/null)
And searching for: App1436 and check the expiration.
![image.png](/.attachments/image-92ef1f5b-2b49-4d76-92a9-8851a58d0151.png)

For Cribl we do receive an email similar to the first one mentioned but also like this:
Subject: **ALERT** AzureAD app credentials nearing expiration [DTTL App1436 Cribl Portal EMEA NONPROD]
![image.png](/.attachments/image-e0db9774-d7b9-4c3f-a2aa-2ec8bdb267dd.png)

## **IMPORTANT**
Run the query below every month to keep track of the certs about to expire also on all three regions:

`index=dttl_internal_* source=cert_expire_check NOT cert_path IN (*peer-apps.old*, *slave-apps.old.bkp*, *slave-apps.old*, */opt/splunk/git/*)
| rex field=_raw "\.pem\s:\snotAfter\=(?<mes>\w+)\s+(?<dia>\d+)\s\d+\:\d+\:\d+\s+(?<ano>\d+)\s"
| rex field=_raw "\.pem\s:\snotAfter\=(?<mes>\w+)\s+(?<dia>\d+)\s(?<H>\d+)\:(?<M>\d+)\:(?<S>\d+)\s+(?<ano>\d+)\s"
| rex field=_raw "\scert_path\s+\=\s(?<cert_path>.*)\s\:"
| eval date_control = now()
| eval today = strftime(date_control, "%d/%m/%Y")
| strcat mes "/" dia  "/" ano " " H ":" M ":" S date_end
| eval date_end2=strptime(date_end, "%b/%d/%Y %H:%M:%S")
| eval diff = date_end2 - date_control
| where diff < 5187390.000000 AND diff  > 0
| eval days_off = round(diff/86400,0)
| table _raw today cert_path host date_control date_end date_end2 diff days_off
| eval instance = if(like(cert_path, "%peer-apps%"), "IDX",if(like(cert_path, "%/splunk/%"), "SE",if(like(cert_path, "%\Splunk\%"), "SE", if(like(cert_path, "%/splunkforwarder/%"), "UF", ""))))
| eval Region =  if(like(host, "ap%"), "APAC",  if(like(host, "CA%") OR like(host, "usa%") OR like(host, "MX%"), "AMER", if(like(host, "eu%"),"EMEA","")))
| stats count by Region host instance cert_path  today date_end  days_off`

![image.png](/.attachments/image-eb8436ef-4d13-40b0-9638-4a50c9206f0e.png)
