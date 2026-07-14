Day 22 – Networking Essentials
Overview

Networking is one of the most important foundations of DevOps, Cloud Computing, and System Administration. Today I learned about network topologies, IPv4 vs IPv6, and commonly used network ports.

1. Types of Network Topology
Bus Topology
All devices connect to a single backbone cable.
Simple and inexpensive.
Failure of the main cable affects the entire network.
Star Topology
All devices connect to a central switch or hub.
Easy to manage and troubleshoot.
Most common topology used in LANs.
Ring Topology
Devices form a circular connection.
Data travels around the ring.
Failure of one node can affect communication unless redundancy exists.

Mesh Topology
Every device connects to multiple devices.
Highly reliable and fault tolerant.
Common in enterprise and data center environments.
Tree Topology
Combination of Star and Bus topology.
Easy to expand.
Suitable for large organizations.
Hybrid Topology
Combination of two or more topologies.
Flexible and scalable.
Used in modern enterprise networks.

2. IPv4 vs IPv6
Feature	IPv4	IPv6
Address Size	32-bit	128-bit
Address Format	Decimal	Hexadecimal
Address Space	~4.3 Billion	Extremely Large
Security	Optional	Built-in IPsec support
Broadcast	Supported	Not Supported (Multicast instead)
NAT	Commonly Used	Generally Not Required

Common Network Ports
Port	Service
20/21	FTP
22	SSH
23	Telnet
25	SMTP
53	DNS
67/68	DHCP
80	HTTP
110	POP3
123	NTP
143	IMAP
161/162	SNMP
389	LDAP
443	HTTPS
