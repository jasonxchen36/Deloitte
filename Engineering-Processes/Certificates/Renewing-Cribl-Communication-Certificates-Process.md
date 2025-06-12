This process describes how to renew the Cribl Communication Core TLS Certificate that is used for communications between Cribl Leader and Cribl Workers.

## **Renew Cribl Communication Certificates**
1. Renew the cert in Venafi and make sure it is signed as server and client auth cert:
openssl x509 -in cribl_communication_core.pem -noout -text
	![image.png](/.attachments/image-1b20e234-c735-408d-92f0-ad8ac7c6e4d0.png)
	
2. Update .crt and .pem file in /opt/cribl-certs on the Cribl Workers (first) and Leader (last):
	**Dev**
	sudo su - dtt_sc_cribl_qa
	vi /opt/cribl-certs/cribl_communication_core.crt
	vi /opt/cribl-certs/cribl_communication_core.pem

	**Prod**
	sudo su - dtt_sc_cribl_prd
	vi /opt/cribl-certs/cribl_communication_core.crt
	vi /opt/cribl-certs/cribl_communication_core.pem

	**Backup**
        mv /opt/cribl-certs/cribl_communication_core.crt /opt/cribl-certs/cribl_communication_core.crt.bak
        mv /opt/cribl-certs/cribl_communication_core.pem /opt/cribl-certs/cribl_communication_core.pem.bak

	**Notes:** 
The .crt and .pem files are the same content and it can be in any order.
Update the cert on all the Cribl Workers first and then do the Cribl Leader last.

3. Restart Cribl:
	logout
	sudo systemctl restart cribl

4. Validate Cribl Workers are reporting to Crib Leader:
Manage > Groups
![image.png](/.attachments/image-fd0c13a8-62a7-4153-9395-7605cec9966c.png)


## **Troubleshooting**
Temporarily disable validate TLS cert for mutual authentication:
Navigate to Settings > Global Settings > Distributed Settings > TLS Settings
![image.png](/.attachments/image-2be7419c-6ea2-4812-a14c-e7cf4ac47e9a.png)
**Note:** Expired certs will work if you disable this setting

Validate TLS certs in the Cribl Workers Groups and make sure the Certificate Name field is BLANK:
Manage > Groups > Click on Worker Group > Group Settings > General Settings > TLS
![image.png](/.attachments/image-6401f628-ac35-4ace-9fcc-ebd796049787.png)

Validate instance.yml:
cat /opt/cribl/local/_system/instance.yml
![image.png](/.attachments/image-27938db6-772f-4a3a-9f96-8e969ab2af6e.png)

Check the Cribl internal logs:
tail -f /opt/cribl/log/cribl.log
cat /opt/cribl/log/cribl.log | grep DistWorker
![image.png](/.attachments/image-f24eb837-3a96-4e7a-8af9-9476913afaa5.png)