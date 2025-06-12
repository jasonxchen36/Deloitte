Splunk Servers in AWS should be created using the Amazon Machine Image available in the GEMS AWS Account. The AMI ID can be found in the AWS VM Inventory sheet. 

Note: Please see the AWS VM Inventory sheet for the information regarding size and type of the EBS Volumes that should be attached to each instance. 

**EBS Volume for Temp should be built as General Purpose GP2 and should only be 32 GiB in size as opposed to the existing old AWS VMs that have 126 GiB of Provisioned IOPS EBS volume for Temp**

Once a server is created, SSH into the server using the credentials below:

User Name: ec2-user
SSH Key: Default regional SSH Key
Password: Not Required

Once logged into the VM via SSH, follow the steps below:

1. Change the hostname of the server:

sudo hostnamectl set-hostname --static aw1436l0**

2. Create a Service Now request for the Linux team so that they can run the post deployment hardening script and also join the VM to the atrame.deloitte.com domain. This request is typically completed by Kyle Harris from the Linux team.

Sample SNow request: 
https://deloitteglobal.service-now.com/sp?id=ticket&table=sc_req_item&sys_id=bb6345a71b920550d14d5281604bcba8&view=closed_portal_tickets

3. Change the /etc/resolv.conf file to add the Global DNS servers.
a.	chattr -i /etc/resolv.conf

    b.	Make changes to the file as per below:

   Contents of resolv.conf:
nameserver 10.241.1.4
nameserver 10.241.1.5
search atrame.deloitte.com
domain atrame.deloitte.com

   c.	chattr +i /etc/resolv.conf

4. Add AWS time source to /etc/chrony.conf

sudo su
vi /etc/chrony.conf
server 169.254.169.123 iburst minpoll 4 maxpoll 4

systemctl restart chronyd
chronyc sources -v

5. Install Splunk using the installer package uploaded on SharePoint

6. Deploy Splunk Web Certificate (All servers except Indexers)

7. Change the splunkd port based on the port available behind the Search Load Balancer (Indexers only) 

8. Change the Indexer clustering attributes for cluster searchability via F5 within the /opt/splunk/etc/system/local/server.conf (Indexer only)

[clustering]
register_forwarder_address = own internal IP
register_replication_address = own internal IP
register_search_address = public IP of F5 for that region

9. Implement firewalld configurations (Cluster Master and Indexers only)
Follow the steps within [this](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/578/Firewalld-Configurations-for-Indexer-Cluster) wiki

10. Remove the splunkforwarder if already present on the server. 
Cloud servers are built with a Splunkforwarder already deployed by configuration management tools. This version of splunkforwarder runs as root user. This needs to be removed and the splunkforwarder version for the core Splunk servers needs to be installed.

11. Ensure that the Splunk server is added behind the Search Load Balancer by adding a new target group for the applicable splunkd port (Indexer only)

12. Add the new indexer IP to outputs.conf within the all forwarder outputs app (Indexer only)

13. DNS request. submit an automated request using the link below:

https://deloitteglobal.service-now.com/sp?id=sc_cat_item&sys_id=fd4e6794db356b0013da10284b9619d5

Sample SNOW request:
https://deloitteglobal.service-now.com/sp?id=ticket&table=sc_req_item&sys_id=2a466f7c879a89507f4364ec8bbb35a6&view=closed_portal_tickets

14. Perform data rebalance for the Indexer Cluster (Only in case of indexer build out)

15. /var/log/messages change

In order to ensure that the /var/log/messages for the core servers are ingested in Splunk, perform the following steps:

a.	sudo setfacl -m g:"dttlatrame service accounts":r /var/log/messages && sudo setfacl -m g:"dttlatrame service accounts":r /var/log/secure && sudo setfacl -m g:"dttlatrame service accounts":r /var/log/cron
b.	cd /etc/logrotate.d/
c.	sudo vi splunk_acl

{
              postrotate
                           /usr/bin/setfacl -m g:"dttlatrame service accounts":r /var/log/messages
                           /usr/bin/setfacl -m g:"dttlatrame service accounts":r /var/log/secure
                           /usr/bin/setfacl -m g:"dttlatrame service accounts":r /var/log/cron
              endscript
}


16. Install Splunk UF on core servers using the UF installer package uploaded on SharePoint (Not applicable for Heavy Forwarders)

17. Integrate the Admin user and password for Splunk within Thycotic

18. Add the VM to the data lifecycle policy 
https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/737/AWS-Data-Lifecycle-Policy-for-Backups

19. Add the indexers to the license pool and increase the daily license limit if required (Only in case of Indexer build out)

20. Add the server to the DS serverclass for core UF

21. Add the server to the regional DMC

22. Submit the SAML FQDN Requests (Not applicable for Indexers)
Sample SNOW request:
https://deloitteglobal.service-now.com/sp?id=ticket&table=sc_req_item&sys_id=49339269871205907f4364ec8bbb352b&view=closed_portal_tickets

23. Configure the DevOps back-up for the Splunk server

24. Purchase the VM for 3 years using AWS Savings Plan if the purchase has been approved via leadership. Follow the steps below:
https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/687/Purchasing-AWS-EC2-Instances-with-AWS-Savings-Plan

25. Update bookmarks wherever needed with new server details

