We have provisioned 2 shared accounts for each environment (Canada DMZ, DMC and Chile) instead of using individual accounts to access their Splunk IFs environment as these Splunk IFs server’s hosting domain is not trusted with our Atrame domain so our Atrame a-* credential won’t work.

These shared accounts secrets are available for entire Engineering team in global thycotic so if anyone check-out these accounts in global thycotic then these accounts won’t be available to other users until they release these accounts by check-in.

Please make sure that you are releasing accounts to other users as soon as your work is done in those environments.

**Canada DMZ Environment**

Shared accounts in Thycotic:
•	caextranet.deloitte.ca\sh-ca_dmz_splunk_pri
•	caextranet.deloitte.ca\sh-ca_dmz_splunk_sec

Jump servers : 
     Canada DMZ Splunk IFs are reachable from our AMER syslog servers (usatramekj037.atrame.deloitte.com, usatramekj038.atrame.deloitte.com) 

Canada DMZ Splunk IFs:
•	CANATLSIS01.caextranet.deloitte.ca (10.54.70.21)
•	CANATLSIS02.caextranet.deloitte.ca(10.54.70.22)
•	CANATLSIS03.caextranet.deloitte.ca(10.54.70.23)
•	CANATLSISR01.caextranet.deloitte.ca(10.60.157.197)
•	CANATLSISR02.caextranet.deloitte.ca(10.60.157.198)
•	CANATLSISR03.caextranet.deloitte.ca(10.60.157.199)

Steps for accessing Canada DMZ Splunk IFs:
•	Login to AMER syslog server using putty with your atrame a-* credential
•	Once you login to syslog server, please connect to Canada DMZ Splunk IF using below command

                       ssh sh-ca_dmz_splunk_pri@caextranet.deloitte.ca@<IP address of Splunk IF>

•	Switch to root or Splunk user account (dtt_sc_splunk_prd@caextranet.deloitte.ca) by entering same shared account password


**Canada DMC Environment**

Shared accounts in Thycotic:
•	hosting.deloitte.ca\sh-ca_dmc_splunk_pri
•	hosting.deloitte.ca\sh-ca_dmc_splunk_sec

Jump server : 
     Canada DMC Splunk IFs are reachable from windows Jump server(10.61.56.204) and this server is reachable from Global VPN. Please use same shared account for login to jump server.

Canada DMC Splunk IFs:
•	CAHOSTDMCSPLUNK1.hosting.deloitte.ca (10.61.117.247)
•	CAHOSTDMCSPLUNK2.hosting.deloitte.ca (10.61.117.248)

Steps for accessing Canada DMC Splunk IFs:

•	Login to Windows Jump server (10.61.56.204) using remote desktop connection(RDP) client  with your shared account credentials like hosting.deloitte.ca\sh-ca_dmc_splunk_pri.
•	Once you login to Jump server, please connect to Canada DMC Splunk IFs using putty client with same shared account like username : sh-ca_dmc_splunk_pri@hosting.deloitte.ca  
•	Switch to root or Splunk user account (dtt_sc_splunk_prd@hosting.deloitte.ca) by entering same shared account password if it prompt for password

**Chile Environment**

Shared accounts in Thycotic:
•	CLEXTRANET.deloitte.com\sh-cl_splunk_pri 
•	CLEXTRANET.deloitte.com\sh-cl_splunk_sec

Jump server : 
     Chile Splunk IFs are reachable directly from global VPN. 

Chile Splunk IFs:
•	CLLSIS01.clextranet.deloitte.com (10.139.11.74)
•	CLLSIS02.clextranet.deloitte.com (10.139.11.75)
    
Steps for accessing Chile Splunk IFs:

•	Login to Chile Splunk IFs with IP address by using putty client with your shared account credentials like sh-cl_splunk_pri@CLEXTRANET.deloitte.com .
•	Switch to root or Splunk user account (dtt_sc_splunk_prd@CLEXTRANET.deloitte.com) by entering same shared account password
