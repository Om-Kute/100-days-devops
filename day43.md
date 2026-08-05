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

⚙️ EC2 Instance Types

EC2 provides different instance families for different workloads.

Category	Typical Use
General Purpose	Web servers, development environments
Compute Optimized	CPU-intensive applications
Memory Optimized	Databases and memory-heavy applications
Storage Optimized	High I/O workloads
Accelerated Computing	GPU, ML, graphics and HPC

The exact instance type should be selected according to workload requirements.

🔑 Key Pairs

Key pairs can be used to authenticate when connecting to Linux EC2 instances.

A key pair consists of:

Public Key
     +
Private Key

The public key is associated with the instance, while the private key must be protected by the user.

Example private key:

mykey.pem

Set restrictive permissions:

chmod 400 mykey.pem

Connect:

ssh -i mykey.pem ubuntu@<PUBLIC-IP>

Never upload your private .pem key to
🛡️ Security Groups

A Security Group acts as a stateful virtual firewall controlling allowed traffic for associated resources such as EC2 network interfaces.

Example inbound rules:

Protocol	Port	Purpose
SSH	22	Remote Linux administration
HTTP	80	Web traffic
HTTPS	443	Secure web traffic

For SSH, prefer:

Port 22
Source → Your trusted IP

instead of exposing SSH to the entire internet.
💾 Amazon EBS

Elastic Block Store (EBS) provides block storage commonly used with EC2.

EBS can store:

Operating system data
Application files
Databases
Logs

EBS volumes can also be backed up using snapshots.

🌐 Elastic IP

An Elastic IP address is a static public IPv4 address provided by AWS.

It can help maintain a consistent public address when associated with supported AWS resources.

Be aware that public IPv4 addresses can incur charges, so unused addresses should not be left allocated unnecessarily.

🔄 EC2 Instance States

Common EC2 states include:

Pending
   │
   ▼
Running
   │
   ▼
Stopping
   │
   ▼
Stopped

An instance can also be:

Shutting-down
Terminated

Once an instance is terminated, it cannot simply be started again.
