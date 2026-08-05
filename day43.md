🚀 Day 43 – AWS EC2 (Amazon Elastic Compute Cloud)
🎯 Objective

Learn how Amazon EC2 provides virtual compute capacity in AWS and understand the components required to securely launch, connect to, and operate an EC2 instance.

Topics Covered
Amazon EC2
AMI
Instance Types
Key Pairs
Security Groups
EBS
Elastic IP
User Data
Instance States
EC2 Purchasing Options
SSH
Nginx Deployment
☁️ What is Amazon EC2?

Amazon Elastic Compute Cloud (EC2) provides scalable compute capacity in AWS.

An EC2 virtual server is called an:

EC2 Instance

EC2 allows us to configure resources such as:

Operating System
      +
vCPU
      +
Memory
      +
Storage
      +
Networking

🏗️ Basic EC2 Architecture
                    Internet
                       │
                       ▼
                Security Group
                       │
                       ▼
                  EC2 Instance
                 /     |      \
                /      |       \
             vCPU    Memory    Network
                       │
                       ▼
                      EBS
📦 AMI – Amazon Machine Image

An AMI provides the information required to launch an EC2 instance.

It can include:

Operating system
Software
Configuration
Root volume information

Examples:

Ubuntu
Amazon Linux
Windows Server
      +
Security
