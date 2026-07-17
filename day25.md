Day 25 – AWS Networking Fundamentals
Objective

Learn the fundamental networking components of AWS and understand how they work together to build secure cloud infrastructure.

1. VPC (Virtual Private Cloud)

A VPC is a logically isolated virtual network where AWS resources are launched.

Features
Isolated from other AWS accounts
Custom IP address range (CIDR)
Full control over routing and security
Supports public and private subnets

2. Subnet

A subnet divides a VPC into smaller networks.

Public Subnet
Connected to an Internet Gateway
Resources are accessible from the Internet
Used for Web Servers, Bastion Hosts, Load Balancers
Private Subnet
No direct Internet access
Used for Databases, Application Servers, Internal Services

3. Route Table

A Route Table contains rules that determine where network traffic should go.

Example:

Destination	Target
10.0.0.0/16	Local
0.0.0.0/0	Internet Gateway (Public)
0.0.0.0/0	NAT Gateway (Private)

4. Internet Gateway (IGW)
An Internet Gateway allows communication between a VPC and the Internet.

Functions
Enables inbound Internet access
Enables outbound Internet access
Used by public subnets

5. NAT Gateway
A NAT Gateway allows instances in private subnets to access the Internet without exposing them to inbound connections.

Common Use Cases
Software updates
Installing packages
Accessing external APIs
