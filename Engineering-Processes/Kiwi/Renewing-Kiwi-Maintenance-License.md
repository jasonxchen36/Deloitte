The following steps below outline how to renew the Kiwi Maintenance License when they expire. 




1. On Splunk server, launch SolarWinds License Manager (should be a shortcut in the start menu on that machine) 

![image.png](/.attachments/image-bf948977-83e5-4c75-b40a-f454543b1468.png)

2. Put a check next to Kiwi Syslog Server and lick “Upgrade” action:



![image.png](/.attachments/image-7381c7c0-4d03-43e4-b8f6-c9dd66cdfd32.png)

3. Here we have two activation options. The first of them, using internet access and an activation key that Daniel Azrak will provide us. The second option is used when we don't have internet access.

- Option 1 (With Internet access and an activation key): Ask **Daniel Azrak** for Activation Key (is the person responsible for supplying this key) and then "Next" button:

![image.png](/.attachments/image-8edcbe85-5863-46b7-b4f4-0362ae79632a.png)

After that, we need to fill in the fields with the following data and click "Next" button:

![image.png](/.attachments/image-b1a9b175-11e6-4dc4-b823-52be5f7f9bf9.png)

**And then Kiwi Maintenance License will be renewed correctly.**

- Option 2 (Without Internet access): Select second option and click "Next" button:

![image.png](/.attachments/image-f94b5411-93f3-4964-94f5-297aa66f1df3.png)

Then, click in "Copy Unique Machine ID" button:

![image.png](/.attachments/image-40303937-c6b6-417e-986b-2b45b9c30f34.png)

Now we have to provide this "Unique Machine ID" to **Daniel Azrak** as he is the responsible for registering this machine on the Solarwinds portal. Once he has registered this "Unique Machine ID", he will provide us with a .lic file which we have to add next in "License Key File location" field and click "Next" button

![image.png](/.attachments/image-ec51a739-b449-4350-aaaa-e15e4338b5a7.png)

**And then Kiwi Maintenance License will be renewed correctly.**

--------------------------------------------------------------
**NOTE:** We can see when the Kiwi license expires at "Kiwi Syslog Service Manager"   ->   "Help"    ->    "About Kiwi Syslog Server"

![image.png](/.attachments/image-960681d8-dd9d-4fc1-95b6-1190a6afb0bf.png)