1)	Write your search as you previously would have 
2)	At some point after the initial tstats search, you will want to correlate an IP address (probably src) with DHCP data. Pipe in the following, which will look at DHCP leases for the past day and correlate a box name:
- | \`microsoft_dhcp_correlation(<ip field to correlate>)`
- Outputs the following:
- "index" field combining base search index with DHCP sub search index into multivalued field
- "host" field containing host that leased / renewed an IP address in DHCP logs over the past day
- Uses an outer join, so will not remove results if there wasn't a correlation between input IP field and DHCP data
3)	Include “host” in your final fields command
