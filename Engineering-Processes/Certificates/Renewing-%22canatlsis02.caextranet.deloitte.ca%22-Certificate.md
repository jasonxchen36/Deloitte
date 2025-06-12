The following steps below outline how to renew and replace "canatlsis02.caextranet.deloitte.ca" certificate.

NOTE: Renewed certificate must be placed in "canatlsis02.caextranet.deloitte.ca" (10.54.70.22) server:

----------------------------

1. First of all, we have to renew this certificate in Venafi (search certificate by "canatlsis02").

      ![image.png](/.attachments/image-c1ac7f6b-3ee2-408d-9fbd-599099c75c73.png)

2. Configuration for downloading the renewed certificate once it is approved:

   ![image.png](/.attachments/image-fe9b3fe9-6a11-4ae2-ac21-ed391b76a361.png)

Note: In this renewed certificate that we have downloaded, we have 4 diferent blocks: the first three corresponding to deloitte, and the last one to the machine itself.

3. For accessing the "CANATLSIS02.caextranet.deloitte.ca" server:
-    Login to AMER syslog server (usatramekj037 or usatramekj038) using putty with your atrame a-* credential

- Once you login to syslog server, please connect to Canada DMZ Splunk IF using below command:
                   ssh sh-ca_dmz_splunk_pri@caextranet.deloitte.ca@10.54.70.22  or  ssh sh-ca_dmz_splunk_sec@caextranet.deloitte.ca@10.54.70.22

- Switch to root or Splunk user account (dtt_sc_splunk_prd@caextranet.deloitte.ca) by entering same shared account password

NOTE: "sh-ca_dmz_splunk_pri" and "sh-ca_dmz_splunk_sec" passwords are in Thycotic

4. Go to /etc/rsyslog.d
Here we should have the following files:
• canatlsis02.caextranet.deloitte.ca.pem
• canatlsis02-cert.pem

5. Backup of both certificates "canatlsis02.caextranet.deloitte.ca.pem" and "canatlsis02-cert.pem"
mv canatlsis02.caextranet.deloitte.ca.pem canatlsis02.caextranet.deloitte.ca.pem.bck
mv canatlsis02-cert.pem canatlsis02-cert.pem.bck

6. Generate a new "canatlsis02.caextranet.deloitte.ca.pem" with the following order:
vi canatlsis02.caextranet.deloitte.ca.pem

ORDER:
- subject=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com
- subject=CN=Deloitte SHA2 Level 2 CA 1, DC=Deloitte, DC=com
- subject=CN=Deloitte SHA2 Level 3 CA 1, DC=atrame, DC=deloitte, DC=com

7. Generate a new "canatlsis02-cert.pem" with the following order:
vi canatlsis02-cert.pem

ORDER:
- subject=CN=canatlsis02.caextranet.deloitte.ca, OU=DTS, O=Deloitte, L=Glen Mills, S=PA, C=US


8. Restart rsyslog service
service rsyslog restart

9. Check for any rsyslog error after renewing certificate
service rsyslog status

10. Check if we are receiving logs as expected in the index "ca_network_cisco_ise"

![image.png](/.attachments/image-61f55942-899f-4055-8b84-4009b2d224f7.png)