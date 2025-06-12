###What: this document defines the changes made at the OS level needed for secmon alerts to function as expected 

###Change needed: (on RHEL) /etc/security/limits.conf 
- Add "* hard maxlogins 1"
- Add "dtt_sc_splunk_prd hard maxlogins 1"

###Also added below configurations to the servers in order to close the ssh session during network interuptions.

echo 600 > /proc/sys/net/ipv4/tcp_keepalive_time
echo 60 > /proc/sys/net/ipv4/tcp_keepalive_intvl 
echo 5 > /proc/sys/net/ipv4/tcp_keepalive_probes