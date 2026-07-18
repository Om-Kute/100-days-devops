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

3. CIDR (Classless Inter-Domain Routing)

CIDR provides flexible IP address allocation and efficient subnetting.

Common CIDR Prefixes
CIDR	Subnet Mask	Usable Hosts
/8	255.0.0.0	16,777,214
/16	255.255.0.0	65,534
/24	255.255.255.0	254
/26	255.255.255.192	62
/30	255.255.255.252	2
Advantages
Efficient IP address utilization
Smaller routing tables
Supports Variable Length Subnet Masking (VLSM)

4. Firewalls
   A firewall filters network traffic according to defined security rules.

Types of Firewalls
Packet Filtering Firewall
Stateful Inspection Firewall
Application Layer Firewall (WAF)
Next-Generation Firewall (NGFW)
Best Practices
Allow only required ports
Block unnecessary traffic
Follow the principle of least privilege
Review firewall rules regularly

Hides internal network addresses
Improves network security
