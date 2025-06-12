To filter out events/results where field values for a given field are internal IPs, run:

| \`internal_ip_space_filter(<target IP field>)`  

in which <target IP field> is the one you want to filter internal IPs from.

This macro will filter everything in the 172.16-31.x.x, 10.x.x.x, and 192.168.x.x space (e.g. all internal IPs).

The macro logic is the following:

[internal_ip_space_filter(1)]
args = target
definition = search NOT [| inputlookup internal_ip_space_filter.csv | rename ip as \$target$ | table \$target$]

The lookup “internal_ip_space_filter.csv” is a csv looking like this:

ip
172.16.0.0/12
10.0.0.0/8
192.168.0.0/16
