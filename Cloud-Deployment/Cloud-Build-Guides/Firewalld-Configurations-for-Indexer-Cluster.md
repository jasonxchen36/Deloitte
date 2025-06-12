# Cluster Master

The Cluster Master (CM) needs to go out to the internet to the Public F5 IP in order to talk to the Indexers. 

In order to solve this issue, we install firewalld on the CM and redirect the outbound traffic with the destination as Public F5 LB IP to the AWS / Azure internal LB. This ensures that the traffic does not leave the cloud. 

Please see below the steps:

Run all the steps below as root user

1. Install firewalld service to the server
yum install firewalld 

2. Unmask firewalld service
systemctl unmask firewalld

3. Start the firewalld service and enable it to start at boot
systemctl start firewalld
systemctl enable firewalld

4. Open port 8000 and 8089 for Splunk web and Splunkd respectively on the firewall
firewall-cmd --zone=public --add-port=8089/tcp --permanent
firewall-cmd --zone=public --add-port=8000/tcp --permanent

5. Reload firewalld service to apply these permanent changes
firewall-cmd  --reload

6. Use firewalld direct rules to redirect the outbound traffic with the destination as Public F5 LB IP to the AWS / Azure internal LB.
firewall-cmd --permanent --direct --add-rule ipv4 nat OUTPUT 0 -d 34.232.226.35 -p tcp -j DNAT --to-destination 10.241.16.132

Note: We have 2 IP addresses (one for each AZ) corresponding to the internal LB in AWS. We just provide the IP in AZ 1 in the direct rule and enable cross-zone load balancing for the load balancer.

7. Ensure that the direct rule has been added
firewall-cmd --direct --get-all-rules
 

# Indexers

Thycotic Servers are integrated with Splunk servers for admin user password rotation. This connection is sent on port 8089 for all Splunk servers. AWS / Azure Indexers run splunkd on custom ports (8289 - 8352)

In order to resolve this issue, we install firewalld on the Indexers and enable port forwarding from 8089 to the respective splunkd port

Please see below the steps:

1. Install firewalld service to the server
yum install firewalld 

2. Unmask firewalld service
systemctl unmask firewalld

3. Start the firewalld service and enable it to start at boot
systemctl start firewalld
systemctl enable firewalld

4. Open ports 9997, 8997, and the splunkd port on the firewall
firewall-cmd --zone=public --add-port=9887/tcp --permanent
firewall-cmd --zone=public --add-port=9997/tcp --permanent
firewall-cmd --zone=public --add-port=[splunkd-port]/tcp --permanent

5. Reload firewalld service to apply these permanent changes
firewall-cmd  --reload

6. Enable masquerade
firewall-cmd --zone=public --add-masquerade --permanent

7. Reload firewalld service to apply these permanent changes 
 firewall-cmd --reload

8. Enable the port forwarding from 8089 to the respective splunkd-port
firewall-cmd --zone=public --add-forward-port=port=8089:proto=tcp:toport=[splunkd-port] --permanent

9. Reload firewalld service to apply these permanent changes 
firewall-cmd --reload
