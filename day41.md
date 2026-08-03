☁️ Day 41 – AWS & Cloud Fundamentals

🎯 Objective

Understand the fundamentals of cloud computing and AWS before working with individual AWS services.

Topics covered:

Cloud Computing
Benefits of Cloud
IaaS, PaaS & SaaS
Cloud Deployment Models
AWS Global Infrastructure
Regions
Availability Zones
Edge Locations
Shared Responsibility Model
☁️ What is Cloud Computing?

Cloud computing is the delivery of computing resources over the internet.

These resources can include:

Servers
Storage
Databases
Networking
Applications
Analytics
Monitoring
Security services

Instead of purchasing and maintaining physical infrastructure, organizations can provision resources from cloud providers when needed.

⚡ Benefits of Cloud Computing
1. Scalability

Resources can be increased or decreased depending on workload requirements.

2. Pay-as-you-go

Organizations generally pay for the resources they consume according to the pricing model of each service.

3. High Availability

Applications can be designed across multiple infrastructure locations to improve availability.

4. Global Reach

Applications can be deployed closer to users around the world.

5. Faster Deployment

   🏗️ Cloud Service Models
IaaS – Infrastructure as a Service

Provides infrastructure resources such as:

Compute
Networking
Storage

AWS examples include:

EC2
EBS
VPC

The customer retains significant control over the operating system, applications, and configurations.

Infrastructure can often be provisioned within minutes.

6. Reduced Hardware Management

Cloud providers manage the underlying physical infrastructure.
PaaS – Platform as a Service
SaaS – Software as a Service

Provides complete applications over the internet.

Users consume the software while the provider manages the underlying application infrastructure.
Provides a managed platform where developers can deploy applications without managing as much of the underlying infrastructure.
🌐 Cloud Deployment Models
Public Cloud

Cloud resources are provided by a third-party cloud provider over shared provider infrastructure.

Examples include:

AWS
Microsoft Azure
Google Cloud
Private Cloud

Cloud infrastructure is dedicated to a single organization.

Hybrid Cloud

Combines private/on-premises infrastructure with public cloud resources.

Multi-Cloud

Uses services from multiple cloud providers.

🌍 AWS Global Infrastructure

AWS infrastructure is organized around concepts including:

AWS Global Infrastructure
        │
        ├── Regions
        │
        ├── Availability Zones
        │
        └── Edge Infrastructure
🌎 AWS Region

A Region is a separate geographic area where AWS operates infrastructure.

Examples:

us-east-1
ap-south-1
eu-west-1

For example:

ap-south-1 → Mumbai

When selecting a Region, organizations may consider:

Latency
Cost
Service availability
Compliance requirements
Data residency requirements

Example:

AWS Elastic Beanstalk
