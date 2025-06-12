The following steps below outline how to replace the Splunk Web certificates when they expire. 

1. Login to the Splunk server and sudo to the Splunk service account (dtt_sc_splunk_prd)

1. Generate Private Key and press [Enter] to skip adding a passphrase:
**_openssl genrsa -out <splunk_hostname>.key 2048_**
Example:
openssl genrsa -out az1436l015.atrame.deloitte.com.key 2048

1. Verify there is no password encrypted on the key:
**_openssl rsa -in <splunk_hostname>.key -text_**
Example:
openssl rsa -in az1436l014.atrame.deloitte.com.key -text

1. Generate Certificate Signing Request (CSR):
**_openssl req -new -key <splunk_hostname>.key -out <splunk_hostname>.csr_**
Example:
openssl req -new -key az1436l014.atrame.deloitte.com.key -out az1436l014.atrame.deloitte.com.csr

1. Input the following fields for the CSR:
C=US, 
ST=PA, 
L=Glen Mills, 
O=Deloitte, 
OU=DTS, 
CN=<splunk server fqdn> (e.g. - aw1436l001.atrame.deloitte.com)
email: dt-cyberdefenseengineering-architecture@deloitte.com
When asked to enter the following values, just hit enter:
![image.png](/.attachments/image-670dbdbf-c371-44fe-9b2d-8218090651f9.png)

1. Email the CSR files to GEMS leadership with access to Venafi. They will upload the files into Venafi, Deloitte's Certificate Authority (CA) and send you signed certificates as .pem files. Configuration for downloading the renewed certificate once it is approved in Venafi:
<IMG  src="https://dev.azure.com/GlobalSOC/93d9ecc1-89fd-4a34-a69b-7282df6fad64/_apis/git/repositories/7c3c331d-0fac-420a-9ad2-1a920f9247d9/Items?path=/.attachments/image-fe9b3fe9-6a11-4ae2-ac21-ed391b76a361.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster"  alt="image.png"/>

1. Open the .pem files in NotePad++ or any text editor and reorganize the certicates in the following order:
   1. Server Certificate
a.	subject=E=dt-cyberdefenseengineering-architecture@deloitte.com, CN=, OU=DTS, O=Deloitte, L=Glen Mills, S=PA, C=US
b.	issuer=CN=Deloitte SHA2 Level 3 CA 1, DC=atrame, DC=deloitte, DC=com
   2.	Level 1 Intermediate Certificate
a.	subject=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com
b.	issuer=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com
   3.	Level 2 Intermediate Certificate
a.	subject=CN=Deloitte SHA2 Level 2 CA 1, DC=Deloitte, DC=com
b.	issuer=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com
   4.	Level 3 Intermediate Certificate
a.	subject=CN=Deloitte SHA2 Level 3 CA 1, DC=atrame, DC=deloitte, DC=com
b.	issuer=CN=Deloitte SHA2 Level 2 CA 1, DC=Deloitte, DC=com


8. Update the auth directory in the Splunk app for web certs with the updated pem file and the key generated in step 2.

9. Update the path in the web.conf file in the Splunk app for web certs accordingly and restart Splunk

------------------------------------

Commands used for Windows instances:

Execute as administrator C:\Program Files\Splunk\bin\openssl.exe
OpenSSL> genrsa -out <hostname>.key 2048 -config "C:\Program Files\Splunk\openssl.cnf"
OpenSSL> rsa -in <hostname>.key -text
OpenSSL> req -new -key <hostname>.key -out <hostname>.csr -config "C:\Program Files\Splunk\openssl.cnf"