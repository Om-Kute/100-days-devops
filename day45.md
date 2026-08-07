🌐 Day 45 – AWS VPC & Networking
🎯 Objective

Learn how Amazon VPC provides a secure and isolated networking environment for AWS resources.

🌐 What is Amazon VPC?

Amazon Virtual Private Cloud (VPC) is a logically isolated virtual network where you can launch AWS resources securely.

It allows you to define:

IP address ranges
Subnets
Routing
Internet connectivity
Network security
🏗️ High-Level Architecture
                    Internet
                        │
                        ▼
               Internet Gateway
                        │
                ┌───────────────┐
                │      VPC      │
                │ 10.0.0.0/16   │
                ├───────────────┤
                │ Public Subnet │
                │ 10.0.1.0/24   │
                │     EC2       │
                ├───────────────┤
                │ NAT Gateway   │
                ├───────────────┤
                │ PrivateSubnet │
                │ 10.0.2.0/24   │
                │ App / Database│
                └───────────────┘
🔢 CIDR Block

CIDR defines the IP address range for your VPC.

Example:

VPC              10.0.0.0/16
Public Subnet    10.0.1.0/24
Private Subnet   10.0.2.0/24

A VPC can contain multiple non-overlapping subnets.

🌍 Public vs Private Subnets
Public Subnet
Route to Internet Gateway
Public IP support
Internet accessible

Typical workloads:

Web servers
Load Balancers
Bastion Hosts
🔒 Private Subnet
No direct internet route
Private IP addresses
Access to the internet through a NAT Gateway if required

Typical workloads:

Databases
Backend APIs
Internal applications

🌐 Internet Gateway (IGW)

Internet Gateway enables communication between a VPC and the internet.

Common route:

Destination     Target
0.0.0.0/0       igw-id
🔄 NAT Gateway

A NAT Gateway allows resources in private subnets to initiate outbound internet connections while preventing unsolicited inbound internet traffic.

Common uses:

OS updates
Package installation
External API access
🛣️ Route Tables

Route tables determine how traffic is forwarded.

Example public route table:

Destination	Target
10.0.0.0/16	local
0.0.0.0/0	Internet Gateway

Example private route table:

Destination	Target
10.0.0.0/16	local
0.0.0.0/0	NAT Gateway

🛡️ Security Groups

Security Groups act as stateful virtual firewalls attached to resources such as EC2.

Example inbound rules:

Port	Purpose
22	SSH
80	HTTP
443	HTTPS
🚧 Network ACLs (NACLs)

Network ACLs operate at the subnet level.

Characteristics:

Stateless
Support allow and deny rules
Separate inbound and outbound rule evaluation
⚖️ Security Groups vs NACLs
Feature	Security Group	Network ACL
Level	Instance	Subnet
Stateful	Yes	No
Allow Rules	Yes	Yes
Deny Rules	No	Yes
🔗 VPC Peering

VPC Peering enables communication between two VPCs using private IP addresses.

Use cases:

Environment separation
Multi-team architectures
Cross-VPC communication
