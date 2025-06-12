This wiki page describes how to install the certificates used for AWS Splunk HEC traffic to the AWS Public LBs.


**Splunk HF certificate.pem order**
1. subject=E=DeloitteGlobalFusionCenterEngineering@deloitte.com, CN=EMEA-PUBHEC-LB-0a7d6c628cc1fcf5.elb.eu-west-2.amazonaws.com, OU=DTS, O=Deloitte, L=Glen Mills, S=PA, C=US
issuer=CN=Deloitte SHA2 Level 3 CA 1, DC=atrame, DC=deloitte, DC=com

2. -----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-256-CBC,FE744A1E26B8CC42B3758AF635FE8F43

3. subject=E=DeloitteGlobalFusionCenterEngineering@deloitte.com, CN=EMEA-PUBHEC-LB-0a7d6c628cc1fcf5.elb.eu-west-2.amazonaws.com, OU=DTS, O=Deloitte, L=Glen Mills, S=PA, C=US
issuer=CN=Deloitte SHA2 Level 3 CA 1, DC=atrame, DC=deloitte, DC=com

4. subject=CN=Deloitte SHA2 Level 3 CA 1, DC=atrame, DC=deloitte, DC=com
issuer=CN=Deloitte SHA2 Level 2 CA 1, DC=Deloitte, DC=com

5. subject=CN=Deloitte SHA2 Level 2 CA 1, DC=Deloitte, DC=com
issuer=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com

6. subject=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com
issuer=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com

**Splunk HF certificate_chain.pem order**
1. subject=CN=Deloitte SHA2 Level 3 CA 1, DC=atrame, DC=deloitte, DC=com
issuer=CN=Deloitte SHA2 Level 2 CA 1, DC=Deloitte, DC=com

2. subject=CN=Deloitte SHA2 Level 2 CA 1, DC=Deloitte, DC=com
issuer=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com

3. subject=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com
issuer=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com

**AWS Public LB certificate order**
Certificate body: Server Certificate from the PEM file
Certificate private key: The decrypted private key for the certificate
Certificate chain (optional): This should be a combination of Level 1 Intermediate Certificate, Level 2 Intermediate Certificate and Root CA Certificate in this same order
1. Server Certificate
	a. subject=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com
	b. issuer=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com
2. Level 1 Intermediate Certificate
	a. subject=CN=Deloitte SHA2 Level 2 CA 1, DC=Deloitte, DC=com
	b. issuer=CN=Deloitte SHA2 Level 1 CA, DC=Deloitte, DC=com
3. Level 2 Intermediate Certificate
	a. subject=CN=Deloitte SHA2 Level 3 CA 1, DC=atrame, DC=deloitte, DC=com
	b. issuer=CN=Deloitte SHA2 Level 2 CA 1, DC=Deloitte, DC=com
4. Root CA Certificate
	a. subject=E=DeloitteGlobalFusionCenterEngineering@deloitte.com, CN=, OU=DTS, O=Deloitte, L=Glen Mills, S=PA, C=US
        b. issuer=CN=Deloitte SHA2 Level 3 CA 1, DC=atrame, DC=deloitte, DC=com

**Verify certificate:**
openssl x509 -in certificate.pem -noout -text 

**Decrypt private key:**
openssl rsa -in <encrypted_private.key>  -out <decrypted_private.key>