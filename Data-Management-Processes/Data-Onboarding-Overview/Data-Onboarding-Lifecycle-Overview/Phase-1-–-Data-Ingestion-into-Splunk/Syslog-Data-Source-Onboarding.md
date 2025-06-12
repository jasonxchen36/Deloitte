#Syslog Data Source Onboarding:

  - Work with data source owner to determine port and protocol (TCP/UDP) for syslog traffic
    - Determine if destination from data source can be configured as an FQDN (preferred method)
  - Configure rsyslog (/etc/rsyslog.d/remote.conf) configuration (listener) on syslog servers in Splunk environment to receive traffic on defined port/protocol
    - Configure log rotate – configure the log rotate time based on the size of the logs and space available on the syslog servers (standard is 3 days)
  - Configure input (usually an app/server class) on the Splunk UF (located on the syslog server) to monitor the new syslog data that is written to the syslog servers
  - For existing or new data source, refer to General steps section below
  - Work with data source owner to validate that logs are being received in Splunk 