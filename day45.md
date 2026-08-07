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
