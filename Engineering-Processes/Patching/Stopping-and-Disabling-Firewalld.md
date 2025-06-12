Firewalld should not be running on any Splunk Deployment Server or Heavy Forwarder

Check the firewalld status:
`sudo systemctl status firewalld`

Stop firewalld for the current session:
`sudo systemctl stop firewalld`

Disable firewalld from starting at boot:
`sudo systemctl disable firewalld`

