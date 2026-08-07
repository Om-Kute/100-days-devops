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
