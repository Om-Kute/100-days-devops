Day 26 – DNS, NAT, CIDR & Firewalls
Objective

Understand four fundamental networking concepts used in Linux, Cloud Computing, AWS, Kubernetes, and DevOps.

1. DNS (Domain Name System)

DNS translates domain names into IP addresses, allowing users to access websites without remembering numerical IP addresses.

Common DNS Record Types
Record	Purpose
A	Maps a domain to an IPv4 address
AAAA	Maps a domain to an IPv6 address
CNAME	Alias for another domain
MX	Mail server record
NS	Authoritative name server
TXT	Verification and security information

2. NAT (Network Address Translation)

NAT enables devices using private IP addresses to access external networks through a public IP address.

Types of NAT
Static NAT – One-to-one mapping
Dynamic NAT – Maps private IPs from a public IP pool
PAT (NAT Overload) – Many private IPs share one public IP using different ports
Benefits
Conserves public IP addresses
Hides internal network addresses
Improves network security
