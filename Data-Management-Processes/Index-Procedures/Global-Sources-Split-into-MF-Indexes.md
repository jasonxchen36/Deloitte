**Global Data Sources that are Split to MF Indexes**

All data from these tools come into Splunk from a global data source which is usually a single source. Once data reaches the Splunk infrastructure, there are configurations in place to separate the data to be in a MF specific index and be routed to the right region. Any troubleshooting required of these datasets, regardless of MF, will need to be looked at from the Splunk server where the feed is originally configured and then if needed go to the global team that manages the tool.

- Firesight 
- Netskope
- Checkpoint - all indexes except:
  - Australia. Australia manages their own CP instance until end of April 2022. It is estimated that starting in May 2022 the AU instance will be managed by Global).
  - Canada.  Canada has a global checkpoint as well as local Checkpoint instance. Please reach out to the local Canada network team (updated contact in Canada contact list) if local Canada Checkpoint feeds are down in Splunk.
  - Switzerland.  Switzerland manages their Checkpoint devices locally.  Please contact the local Swiss network team if the Swiss Checkpoint feeds are down.
- WSS
- Kenna
- Beyond Trust (This feed is configured using one input for each MF/Region)
- Cylance

For historical information, leverage work item where effort of splitting data to MF indexes was tracked https://dev.azure.com/GlobalSOC/Splunk/_workitems/edit/109