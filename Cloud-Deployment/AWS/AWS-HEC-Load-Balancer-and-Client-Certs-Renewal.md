**SSL Certificate Renewal for HEC LBs**

Within the 3 regional AWS environments, we have a Classic Load Balancer that receives HTTP Event Collector data to be ingested in Splunk. In order to receive encrypted data, we have imported SSL certificates for each of the load balancers. 

The certs for the 3 LBs in Venafi are:
- AMER: internal-A1436-AME-HEC-LB-620766561.us-east-1.elb.amazonaws.com.pem
- AMER: AMER-PUBHEC-LB-f9857ebddf0847db.elb.us-east-1.amazonaws.pem
- AMER: AMER-S3HEC-LB-06b3fcfdb031d06c.elb.us-east-1.amazonaws.pem
- EMEA: internal-A1436-EMA-HEC-LB-1356148794.eu-west-1.elb.amazonaws.com.pem
- EMEA: EMEA-PUBHEC-LB-0a7d6c628cc1fcf5.elb.eu-west-2.amazonaws.pem
- EMEA: EMEA-PUBSPL-LB-939b6d38ae77ef7d.elb.eu-west-2.amazonaws.pem
- APAC: internal-A1436-AP-HLB-795177563.ap-northeast-1.elb.amazonaws.com.pem

These certificates need to be renewed every year in Venafi. Please see below the steps for the renewal process:

1. Ask Daisy or Naveen to renew the SSL certificate within Venafi. They will send you the signed renewed certificate as a .pem file
2. Access the GEMS AWS Account via the [AWS Console](https://account.activedirectory.windowsazure.com/r#/applications) and from all the available services, select "Certificate Manager"
3. Make sure that you are in the correct AWS region based on the LB region
4. From the available certificates on that page, select the certificate with the LB domain name and click the available drop down for options
5. Select the "Reimport Certificate" option
6. You will then need to add the relevant certificate contents as below:
   - Certificate body: Should be the Server Certificate from the PEM file
   - Certificate private key: The private key for the certificate (Root CA Certificate)
**Notes: .keys can be found in "aw1436l045" server in "/home/dtt_sc_splunk_qa/build/hec_cert" directory**
   - Certificate chain: This should be a combination of Level 1 Intermediate Certificate, Level 2 Intermediate Certificate and Level 3 Intermediate Certificate in this same order  

**IMPORTANT**

When renewing both AMER-PUBHEC-LB-f9857ebddf0847db.elb.us-east-1.amazonaws.pem and EMEA-PUBSPL-LB-939b6d38ae77ef7d.elb.eu-west-2.amazonaws.pem we should contact Konstantin (kitov@deloitte.com) and David W (ddefibaugh@deloitte.com) with the new certificates.

**SSL Certificate Renewal for HEC Clients**

We also have a common SSL certificate for clients that are sending data to the AWS HEC LBs. The name of this certificate is awsclient.atrame.deloitte.com.pem

See below for the clients using this certificate:

**ForgeRock**
1. ForgeRock Access Management (AM)
2. ForgeRock Identity Management (IdM) 
3. ForgeRock Directory Services (DS) 

**EKS Clusters**
1. AMER EKS Dev Endpoint
2. AMER EKS QA Endpoint
3. AMER EKS Stage Endpoint
4. AMER EKS Prod Endpoint
5. EMEA EKS QA Endpoint
6. EMEA EKS Stage Endpoint
7. EMEA EKS Prod Endpoint
8. APAC EKS Stage Endpoint
9. APAC EKS Prod Endpoint


This client certificate needs to be renewed every year in Venafi. Ask Daisy or Naveen to renew the SSL certificate within Venafi. They will send you the signed renewed certificate as a .pem file

Please see below the steps for the renewal process:

**ForgeRock AM, IDM and DS**

- Send the renewed certificate along with the private key to the CIAM team. The CIAM team will update this certificate within the ForgeRock AM, IDM and DS certificate stores.

**EKS Clusters**
- In order to update this renewed certificate for the all the Kubernetes clusters across the 3 regions, you will have to update the certificate details within the yaml files used to deploy the Splunk Connect for Kubernetes app for all the clusters.  

- Within the yaml file for each Kubernetes cluster, add the components of the certificate as mentioned below:
1. clientCert - Add only the client certificate without the certificate chain within the clientCert field within the yaml file
2. clientKey - Add the private key of the certificate within this field in the yaml file
3. caFile - Add the certificate chain within the caFile field in the yaml file.

- Repeat this process for all the Kubernetes clusters and provide the updated yaml files to the CIAM team POC

- The CIAM team will then re-deploy the Splunk Connect for Kubernetes app on all the Kubernetes cluster by using the updated yaml files containing the updated certificate.


### **Token troubleshooting**

Recently we had an issue renewing the EKS clusters certificate because the token wasn't working and we were not receiving any events so we had to renew it, here are the steps for renewing the token in case that it doesn't work:

1. First you need to check in the AWS DS on which HFs is the HEC app deployed.
2. Then check that the token that you are using is the same as the one inside the app folder. If not, edit the token with the one that you are using. _(You can check the tokens on any SH in the tokens tab)_
3. If the token doesn't work and you need to renew it go to Settings>Tokens>Create a new token, then create the token with the same configuration as the previous one (_you can check it on the same tab)_ and then disable the old token.
4. Log in via backend and paste the token that you have just created into the HEC application.




