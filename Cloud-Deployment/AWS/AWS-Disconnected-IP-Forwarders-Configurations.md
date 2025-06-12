Below are the different zone configurations for HEC traffic on the AWS disconnected IP forwarders.


**AMER AWS IP FORWARDER 1 - aw1436l100**
00-dev
sudo firewall-cmd --permanent --new-zone="00-dev"
sudo firewall-cmd --add-source "34.67.106.64/28" --zone="00-dev" --permanent
sudo firewall-cmd --permanent --zone=00-dev --add-forward-port=port=8088:proto=tcp:toport=8087:toaddr=10.224.13.231
sudo firewall-cmd --zone=00-dev --permanent --add-masquerade
sudo firewall-cmd --zone=00-dev --add-port=8088/tcp --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --list-all-zones

public
sudo firewall-cmd --permanent --zone=public --add-forward-port=port=8088:proto=tcp:toport=8088:toaddr=10.224.13.231
sudo firewall-cmd --zone=public --add-port=8088/tcp --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --list-all-zones


**AMER AWS IP FORWARDER 2  - aw1436l101**
00-dev
sudo firewall-cmd --permanent --new-zone="00-dev"
sudo firewall-cmd --add-source "34.67.106.64/28" --zone="00-dev" --permanent
sudo firewall-cmd --permanent --zone=00-dev --add-forward-port=port=8088:proto=tcp:toport=8087:toaddr=10.224.13.253
sudo firewall-cmd --zone=00-dev --permanent --add-masquerade
sudo firewall-cmd --zone=00-dev --add-port=8088/tcp --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --list-all-zones

public
sudo firewall-cmd --permanent --zone=public --add-forward-port=port=8088:proto=tcp:toport=8088:toaddr=10.224.13.253
sudo firewall-cmd --zone=public --add-port=8088/tcp --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --list-all-zones