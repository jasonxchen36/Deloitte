This wiki page describes how to configure the firewalld on IP Forwarders in the Azure environment. The IP Forwarders are hosted in various Azure regions and used to ingest OS logs from different global member firms.

1. SSH into the server using your Deloitte privileged credentials (a-account)
2. Install firewalld service to the server:
`sudo yum install firewalld`


3. Start firewalld service:
`sudo systemctl start firewalld`

4. Enable firewalld service:
`sudo systemctl enable firewalld`

5. Enable service to start at boot:
`sudo vi /etc/sysctl.conf`

   Change to 1 under "Controls IP packet forwarding"
   `net.ipv4.ip_forward = 1`

5. Open port 8089 for splunkd management and 9997 for splunk forwarding:

```
sudo firewall-cmd --permanent --zone=public --add-forward-port=port=9997:proto=tcp:toport=9997:toaddr=<to_address>
sudo firewall-cmd --permanent --zone=public --add-forward-port=port=8089:proto=tcp:toport=8089:toaddr=<to_address>
sudo firewall-cmd --permanent --zone=public --add-rich-rule="rule family="ipv4" source address=<source_address> port protocol="tcp" port="9997" accept"
sudo firewall-cmd --permanent --zone=public --add-rich-rule="rule family="ipv4" source address=<source_address> port protocol="tcp" port="8089" accept"
```


   **Notes:**
**`<to_address>`** is IP address of Azure LB in the region where Splunk is located. For example, APAC = Southeast Asia = 10.240.214.42

   **`<source_address>`** is IP address of Azure LB in the region where the incoming network traffic is coming from. For example, Japan East = 10.122.172.4


 **Example for IP Forwarder in Japan East region:**

```
sudo firewall-cmd --permanent --zone=public --add-forward-port=port=9997:proto=tcp:toport=9997:toaddr=10.240.214.42
sudo firewall-cmd --permanent --zone=public --add-forward-port=port=8089:proto=tcp:toport=8089:toaddr=10.240.214.42
sudo firewall-cmd --permanent --zone=public --add-rich-rule="rule family="ipv4" source address=10.122.172.4  port protocol="tcp" port="9997" accept"
sudo firewall-cmd --permanent --zone=public --add-rich-rule="rule family="ipv4" source address=10.122.172.4  port protocol="tcp" port="8089" accept"
```


6. Add masquerade for the added rules
`sudo firewall-cmd --zone=public --permanent --add-masquerade`

7. Open port 1270 for SCOM connection:



```
sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="10.236.161.168" port protocol="tcp" port="1270" accept'
sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="10.236.160.190" port protocol="tcp" port="1270" accept'
sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="10.247.161.147" port protocol="tcp" port="1270" accept'
sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="10.247.161.50" port protocol="tcp" port="1270" accept'
```




8. Reload firewalld service to apply these permanent changes
`sudo firewall-cmd --reload`

8. Reboot the server and verify all the configurations are working as expected:
`sudo reboot`
`sudo firewall-cmd --state`
`sudo firewall-cmd --list-all`
`sudo cat /etc/sysctl.conf`



