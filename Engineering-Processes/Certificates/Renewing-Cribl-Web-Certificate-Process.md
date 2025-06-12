This process describes how to renew the Cribl Web TLS Certificate that is used for the GUI on the Cribl Leader.
1. Renew the certificate in Venafi and make sure it is signed as a "TLS Web Server Authentication"
2. Add the certificate to the Cribl Leader:
Settings > Global Settings > Security > Certificates and click "Add Certificate"
![image.png](/.attachments/image-98cd949f-526b-4956-89e0-58281d2e0e35.png)
3. Input the following information and click "Save":
![image.png](/.attachments/image-a016c95d-7b30-436f-83e3-9b791b6026ed.png)
    - Name: cribl_web_<YYYY>
    - Description: Deloitte signed web certificate <YYYY>
    - Certificate: Directly copy the contents in the certificate pem file and paste it in. The order does not matter.
    - Private Key: You can find the key by running these commands on the Leader via SSH.

       ```
       sudo su - dtt_sc_cribl_qa
       sudo su - dtt_sc_cribl_prd
       cat /opt/cribl/local/cribl/auth/certs/cribl_web.key
       ```

   - CA certificate: Directly copy the contents in the certificate pem file and paste it in. The order does not matter.
4. Switch over to the new certificate from the drop down menu on "Certificate name":
Settings > Global Settings > General Settings > API Server Settings > TLS
![image.png](/.attachments/image-c28404d4-5372-44e6-800d-ab4366dbdf00.png)
5. Click save and the pop message will ask to restart the Leader and click "Yes".
6. Validate the certificate is working by going into Certificate Viewer on your browser (screenshot is using Google Chrome).
![image.png](/.attachments/image-944c9905-76fb-46f3-87e9-c18d922fe3f0.png)