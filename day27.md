Day 27 – 20 Essential Linux Networking Commands
Objective

Learn the most commonly used networking commands for Linux administration, troubleshooting, cloud computing, and DevOps.

Command	Purpose
ip a	Show IP addresses and interfaces
ip route	Display routing table
ip link	Manage network interfaces
ip neigh	Show neighbor (ARP) table
arp -a	Display ARP cache
dig domain.com	DNS lookup
host domain.com	Resolve hostname
traceroute domain.com	Trace network path
tracepath domain.com	Trace path without root
tcpdump -i eth0	Capture network packets
lsof -i	Show open network connections
nc -zv host port	Test TCP/UDP port connectivity
ethtool eth0	Display NIC information
nmcli device status	Show network device status
resolvectl status	Show DNS resolver configuration
mtr domain.com	Network diagnostics
iperf3 -s	Start bandwidth server
iperf3 -c server-ip	Test network bandwidth
iftop	Monitor live network traffic
vnstat	View historical network usage
