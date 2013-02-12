= About

FireWall Object Verifier fwov is a tool to help some operational challenges on firewalls. 

On a firewall you typically have objects that consist of an IP an a name. This name is usually just a label and only the IP is he info that really matters for the firewall.
This label can be the name of the machine or its an operational name like "mailserver". The discussion of how to create names is a different topic, you may see Tom Limoncellis [The Practice of System and Network Administration(http://www.everythingsysadmin.com/) 

Sometimes the label is the name of a system that ownded this IP ten years ago, and this is where the fun starts.

Systems are migrated or deconfigured, names and IPs reused. Also, think about all thouse places where the relationship name->IP is used. There are places like your firewalls, DNS, [CMDBs](http://en.wikipedia.org/wiki/CMDB), [IPAM (the Excelsheet)](http://en.wikipedia.org/wiki/Internet_Protocol_Address_Management), ...

So, here is the goal of fwov: set up a database of objects and notify the user of disputes. Maybe export to ruleset in a far future.

= Architecture

== .fwovrc

# List off all domainsuffixes used in your organisation
domainsuffixes = domain1, domain2
# Database stuff
dbuser
dbpass
# various paths
zonefiles ...
# max age of dns entries
dnsage = 

== Database

* postgresql

    objectid
    name
    comment
    ip
    ip-reverse
    domainN-name + timestamps
    domainN-ip
    domainN-reverse
    ignore

== Importer

* Bind-Zonefiles
* CheckPoint
* Cisco ASA
* iptables ferm
* ...

== Worker

* DNS lookups if timestamp older than dnsage
* one worker per domain

== Reports

* List of all disputed objects
* one mail per object to create tickets
* List of disappeared objects

= IPv6

fwov cares about IPv6 and so should you

= Disclaimer

Noob at work, no guarantees at all.
If you know a similar project, please let me know

= Licence

Not yet decided yet, but will be open (GNU, APache, BSD)
