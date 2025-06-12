Below are the different zone configurations for HEC traffic on the Azure disconnected IP forwarders.

Apply both zone configurations on each host:
- EMEA Azure IP FORWARDER 1 - az1436l134
- EMEA Azure IP FORWARDER 2 - az1436l135

## **00-dev**

```
sudo firewall-cmd --permanent --new-zone="00-dev"
sudo firewall-cmd --add-source 12.97.57.82 --zone="00-dev" --permanent
sudo firewall-cmd --permanent --zone=00-dev --add-forward-port=port=8088:proto=tcp:toport=8087:toaddr=10.235.136.220
sudo firewall-cmd --permanent --zone=00-dev --add-rich-rule="rule family="ipv4" source address=12.97.57.82 port protocol="tcp" port="8088" accept"
sudo firewall-cmd --zone=00-dev --permanent --add-masquerade
sudo firewall-cmd --zone=00-dev --add-port=8088/tcp --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --list-all-zones
```

---


## **public**

```
sudo firewall-cmd --permanent --zone=public --add-forward-port=port=8088:proto=tcp:toport=8088:toaddr=10.235.136.220
sudo firewall-cmd --zone=public --add-port=8088/tcp --permanent
sudo firewall-cmd --permanent --zone=public --add-rich-rule="rule family="ipv4" source address=20.105.88.163 port protocol="tcp" port="8088" accept"
sudo firewall-cmd --permanent --zone=public --add-rich-rule="rule family="ipv4" source address=20.105.88.163 port protocol="tcp" port="8087" accept"
sudo firewall-cmd --reload
sudo firewall-cmd --list-all-zones
```