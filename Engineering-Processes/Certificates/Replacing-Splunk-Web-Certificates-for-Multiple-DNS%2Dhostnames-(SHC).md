The following steps below outline how to replace the Splunk Web certificates when they expire.
This procedure cover the case when is necessary create a certificate for differents hosts or with different DNS. Is the typical case of Search Head Cluster, where there are many host and a public DNS.
 
1. Update the openssl.cnf file, by default in Splunk environment is in **/opt/splunk/openssl/openssl.cnf**, in the line 217 there is the configuration that need to add:

**NOTE:** In the following links, is explained in details.
- https://answers.splunk.com/answers/476596/how-to-generate-csr-files-with-subjectaltnames-san.html
- http://wiki.cacert.org/FAQ/subjectAltName

//////////////////////////////////////////////////////////////////////////////////////
Below must be added in _**[ v3_req ]**_ stanza:

subjectAltName = @alt_names

[alt_names]
DNS.1 = splunkadhoc.atrame.deloitte.com
DNS.2 = splunkadhoc
DNS.3 = usatramekj034.atrame.deloitte.com
DNS.4 = usatramekj034
DNS.5 = usatramekj035.atrame.deloitte.com
DNS.6 = usatramekj035
DNS.7 = usatramekj036.atrame.deloitte.com
DNS.8 = usatramekj036
DNS.9 = usatramekj134.atrame.deloitte.com
DNS.10 = usatramekj134
DNS.11 = usatramekj135.atrame.deloitte.com
DNS.12 = usatramekj135

//////////////////////////////////////////////////////////////////////////////////////

The result should be like the following screenshot:

![image.png](/.attachments/image-37ec3ced-eaca-415d-93bf-c39f5e9ca7e8.png)

2. Login to the Splunk server and sudo to the Splunk service account (dtt_sc_splunk_prd)

3. Generate Private Key and press [Enter] to skip adding a passphrase:
**_openssl genrsa -out <splunk_hostname>.key 2048_**
Example:
openssl genrsa -out QA_SHC_AMER.atrame.deloitte.com.key 2048

4. Verify there is no password encrypted on the key:
**_openssl rsa -in <splunk_hostname>.key -text_**
Example:
rsa -in QA_SHC_AMER.atrame.deloitte.com.key -text

**NOTE:** Steps 3 and 4 can be done using the deloitte.key deployed with the splunkweb_ssl app:

./splunk cmd openssl req -new -key /opt/splunk/etc/apps/del_stage_prod_splunkweb_ssl /auth/deloitte.com.web.key -out /opt/splunk/etc/auth/mycerts/QA_SHC.csr

5. Generate Certificate Signing Request (CSR):
**_openssl req -new -key <splunk_hostname>.key -out <splunk_hostname>.csr_**
Example:
openssl req -new -key QA_SHC_AMER.atrame.deloitte.com.key -out QA_SHC_AMER.csr

6. Input the following fields for the CSR:
C: US 
ST: PA 
L: Glen Mills 
O: Deloitte 
OU: DTS 
CN: splunkadhoc.atrame.deloitte.com 
Email Address: dt-cyberdefenseengineering-architecture@deloitte.com

![image.png](/.attachments/image-f7109c19-0e28-49b7-a522-379c9f7fa3e1.png)

When asked to insert the following info, just press enter:

![image.png](/.attachments/image-34008637-0aea-4005-87aa-bdcd7743e6ea.png)

This creates a QA_SHC.csr file, is a good practice check the result, we can do that coping the result of .csr in the web https://www.sslshopper.com/csr-decoder.html

![image.png](/.attachments/image-ee1331d5-dcbd-4a69-a3b9-b5b7bce8384a.png)


**NOTE: Is very important to check that all names are present.**

7. Email the CSR files to Daisy and Naveen. They will upload the files into Venafi, Deloitte's Certificate Authority (CA) and send you signed certificates as .pem files. Configuration for downloading the renewed certificate once it is approved in Venafi:
<IMG  src="https://dev.azure.com/GlobalSOC/93d9ecc1-89fd-4a34-a69b-7282df6fad64/_apis/git/repositories/7c3c331d-0fac-420a-9ad2-1a920f9247d9/Items?path=/.attachments/image-fe9b3fe9-6a11-4ae2-ac21-ed391b76a361.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster"  alt="image.png"/>

1. Open the .pem files in NotePad++ or any text editor and reorganize the certicates in the following order:
- Server Certificate
- Level 1 Intermediate Certificate
- Level 2 Intermediate Certificate
- Level 3 Intermediate Certificate
- You can verify this with the following web https://www.sslshopper.com/certificate-decoder.html

![image.png](/.attachments/image-d15dc552-81df-456f-a2d4-d53ec1ff27ca.png)

![image.png](/.attachments/image-a463aa78-08dd-4e16-92ba-c9fd9cfe0f3d.png)

- Other point to check is if the certificate has a Subject and Issuer lines, if exits 
this must be deleted it

![image.png](/.attachments/image-31b8efc8-8a5c-452e-a6fc-c176ccaea398.png)

9. Update the auth directory in the Splunk app for web certs with the updated pem file and the key generated in step 3.
- /opt/splunk/etc/apps/del_stage_prod_splunkweb_ssl /auth/
- and update web.conf in /opt/splunk/etc/apps/del_stage_prod_splunkweb_ssl /local/web.conf

![image.png](/.attachments/image-608747f9-1716-41c6-9ec2-30c625479403.png)

- Finally is necessary to restart splunk service, **in case we are working in a SHC, is necessary to deploy by Deployer.**

10. After that, we verify that the access by browser works fine, and does not appear a warning.
 
![image.png](/.attachments/image-1786762c-5b2f-4f22-8e26-92f370cf63ba.png)
