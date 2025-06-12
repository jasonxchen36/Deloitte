The following steps below outline how to renew and replace "**Splunk _Wildcard_Prod_External**" certificate. 

NOTE: Renewed certificate must be placed in the following server:
- Usatramekj179 and usatramekj180
- Eu1436l041, eu1436l042, eu1436l043, eu1436l044, eu1436l077, eu1436l078, eu1436l079 and eu1436l080

------------------
-----------------
1.	First of all, we have to renew this certificate in Venafi (search certificate by "Splunk _Wildcard_Prod_External". As this is an external certificate, we need the approval by Cybersecurity Ops: check approver on snow incident or task

2.	Configuration for downloading the renewed certificate once it is approved:

![image.png](/.attachments/image-6c9d571b-57f5-4c12-a3fc-b55289b136ef.png)
Note: you can use any password (but don't forget it) because we will download it with any password and then we will delete the password from the key in one step later (step 9).

Note: In this renewed certificate that we have downloaded, we have **4 diferent blocks**: the first and second blocks are corresponding to “entrust_wildcard_new_root.pem” certificate, the third correspond to “entrust_wildcard_new_cert.pem” and the fourth corresponds to the encrypted key “entrust_wildcard_new.key” (it is located at the end of the file)

3.	SSH to the servers
4.	Sudo as root
sudo su
5.	Go to /etc/rsyslog.d
6.	Here we should have the following files:
•	entrust_wildcard_new_cert.pem
•	entrust_wildcard_new.key
•	entrust_wildcard_new_root.pem
7.	Backup of “entrust_wildcard_new.key”   
mv entrust_wildcard_new.key entrust_wildcard_new.key.bak
8.	Generate a new “entrust_wildcard_new.key” with the renewed generate key obtained in step 3 (**Fourth block** of the certificate downloaded in step 3)
vi entrust_wildcard_new.key

![image.png](/.attachments/image-b75776c5-0322-4aff-a1c9-2587f2087dca.png)

9.	Remove the password from key:
openssl rsa -in entrust_wildcard_new.key -out new.key 

Note: Here it will ask us to enter the password that we have put in step 2

10.	Rename the “new.key” again as “entrust_wildcard_new.key”
mv new.key entrust_wildcard_new.key

11.	Backup of “entrust_wildcard_new_root.pem”   
mv entrust_wilsdcard_new_root.pem  entrust_wildcard_new_root.pem.bak

12.	Generate a new “entrust_wildcard_new_root.pem” with the renewed generate certificate in step 3 (**First and second blocks** of the certificate downloaded in step 3)
vi entrust_wildcard_new_root.pem

13.	Backup of “entrust_wildcard_new_cert.pem”   
mv entrust_wildcard_new_cert.pem  entrust_wildcard_new_cert.pem.bak

14.	Generate a new “entrust_wildcard_new_cert.pem” with the renewed generate certificate in step 3 (**Third block** of the certificate downloaded in step 3)
vi entrust_wildcard_new_cert.pem

15.	Restart rsyslog service
service rsyslog restart

16.	Check for any rsyslog error after renewing certificate
service rsyslog status

16.	Check if we are receiving logs as expected after renewing certificate
cd /opt/splunkforwarder/var/syslog/SEPMobile  (for example)
