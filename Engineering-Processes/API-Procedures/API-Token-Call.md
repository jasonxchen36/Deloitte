In case it will be necessary to create or migrate an user account for API call to Splunk, it is necessary to use TOKEN instead user/password.

Here steps:

- First, it is necessary to check if token authentication is enable or disable, by default is disabled

          /opt/splunk/bin/splunk btool authorize list tokens_auth --debug
![image.png](/.attachments/image-171521fb-6795-4efd-a367-2cb65ed6d9a1.png)

- Now we need to verify is the user was created, and if has the correct roles assigned, it is important to has the roleof the idnexes and the api role

![image.png](/.attachments/image-8a945fe6-0500-4a52-90dc-ad2d0a8cb21e.png)

- After enable and verify it, we can go ahead with token creation:



![image.png](/.attachments/image-d330d676-bd8a-4144-9527-b7f46d9d733f.png)
![image.png](/.attachments/image-f1832d17-ab0c-463f-a9b0-e64cfef84f95.png)

- It is mandatory to setup existing **User** and **Audience**, in case it will be necessary it is possible to setup a  experiration time.

![image.png](/.attachments/image-efac22b6-dbbf-48d3-9016-c82fae874a65.png)

- After click in **Create** it is possible see the token, **here is the only moment when is possible to view and copy the token** so need to copy and save the token

- Then, from GUI we can disable, enable or remove the token:

![image.png](/.attachments/image-5cce4234-a7f9-4d88-b422-9968708b4d60.png)

- Finally, we can verify if token is working running the token from backend

![image.png](/.attachments/image-7c118213-3383-4910-a4d6-613dbf582a79.png)

More details and information here: https://docs.splunk.com/Documentation/Splunk/9.2.0/Security/UseAuthTokens

**NOTE:** Details about contacts for accounts are in **Splunk Data Flow Options - Global.pptx** file

# Thycotic secret creation.

- First of all we need to access to our thycotic account. Once we are at the thycotic page, make sure you will create the secret on the wanted folder. For example:

![image.png](/.attachments/image-986c6699-ccf9-49e2-b4cd-c3afcfee2b4e.png)

- Once we are at the correct folder, in order to create the secret click on the top right plus icon.

![image.png](/.attachments/image-3fb7c693-1038-44ee-8b79-ed954074bb86.png)

- Here, you need to select the template for splunk.

![image.png](/.attachments/image-48e210e2-e2df-4be9-b7cb-b3ddfcae00c1.png)

- After clicking on it, we well fill the inputs and paste or create the password. In our case we will put on the password input the token.

![image.png](/.attachments/image-680eb573-41a4-484f-91d9-b03280b21ff9.png)

- Now that the secret has been created we will need to make sure everyone needed has the permissions to view the token. On our secret we will go to the Sharing option and then on Edit.

![image.png](/.attachments/image-0e43c10f-345a-4113-8d81-f274a71e6c9b.png)

- Here, we will add the users and allow them only to view the token so the **ROLE** is important to be set to **VIEW**.

![image.png](/.attachments/image-d12bf318-c31a-4c1a-8011-c3fb3d6ea17d.png)
![image.png](/.attachments/image-f53712ab-7c22-4ddb-abf0-8dc16bbce023.png)



