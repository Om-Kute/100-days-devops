Day 24 – IP Addressing Fundamentals
Objective

Learn the fundamentals of IP addressing, including Public vs Private IP, Static vs Dynamic IP, and IPv4 Address Classes.

What is an IP Address?

An IP (Internet Protocol) Address is a unique numerical identifier assigned to every device connected to a network. It allows devices to communicate with each other over local networks and the Internet.

1. Public IP vs Private IP
Public IP
Assigned by an Internet Service Provider (ISP)
Globally unique
Used for Internet communication
Example: 8.8.8.8
Characteristics
Accessible over the Internet
Used by websites, cloud servers, and public services
Private IP
Used within local networks
Not routable on the Internet
Assigned by routers or DHCP servers
Private IP Ranges
Range	CIDR
10.0.0.0 – 10.255.255.255	/8
172.16.0.0 – 172.31.255.255	/12
192.168.0.0 – 192.168.255.255	/16
2. Static IP vs Dynamic IP
Static IP
Fixed IP address
Manually configured
Best for servers, routers, websites, databases, and CCTV
Dynamic IP
Automatically assigned by DHCP
Changes over time
Commonly used for personal devices

3. IPv4 Address Classes
Class	Range	Default Subnet Mask	Usage
A	1–126	255.0.0.0 (/8)	Large Networks
B	128–191	255.255.0.0 (/16)	Medium Networks
C	192–223	255.255.255.0 (/24)	Small Networks
D	224–239	N/A	Multicast
E	240–255	N/A	Experimental
