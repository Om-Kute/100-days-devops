🚀 Day 47 – AWS RDS & Route 53
🎯 Objective

Learn how Amazon RDS provides managed relational databases and how Amazon Route 53 provides DNS and traffic-management capabilities.

🗄️ Amazon RDS

Amazon Relational Database Service (RDS) is a managed service for running relational databases in AWS.

AWS handles many infrastructure-management tasks such as:

Provisioning
Database software setup
Automated backups
Patching
Monitoring integrations
Infrastructure maintenance
🛢️ Supported Database Engines

Common RDS engines include:

MySQL
PostgreSQL
MariaDB
Oracle
Microsoft SQL Server
Amazon Aurora
⭐ RDS Features
🔄 Automated Backups

RDS can automatically back up supported database instances and provide point-in-time recovery within the configured retention period.

📸 DB Snapshots

Manual snapshots can be created for backup and recovery.

🔐 Encryption

RDS supports encryption at rest using AWS Key Management Service (KMS).

Encryption in transit can also be configured for supported engines.

📊 Monitoring

RDS integrates with Amazon CloudWatch for metrics and monitoring.

🛡️ High Availability

Multi-AZ deployments can provide standby infrastructure for automatic failover.
🔄 Multi-AZ vs Read Replica
Feature	Multi-AZ	Read Replica
Main Purpose	High availability	Read scalability
Primary Benefit	Failover	Read performance
Replication	Synchronous for supported configurations	Asynchronous
Typical Use	Production HA	Read-heavy workloads
Simple Architecture
             Multi-AZ
        ┌───────────────┐
        │               │
        ▼               ▼
   Primary RDS       Standby
      AZ-A              AZ-B
        │               │
        └── Failover ───┘
Read Replica
             Primary
                │
       ┌────────┴────────┐
       ▼                 ▼
 Read Replica 1     Read Replica 2

Read replicas are useful for scaling read-heavy workloads.
💾 RDS Backups
Automated Backups

Used for:

Point-in-time recovery
Automated backup management
Disaster recovery
DB Snapshots

Manual snapshots can be retained for longer-term backup requirements.
🌐 Amazon Route 53

Amazon Route 53 is a highly available and scalable Domain Name System (DNS) service.

It can provide:

Domain registration
DNS hosting
DNS resolution
Health checks
Traffic routing
🧩 Route 53 Components
Route 53
   │
   ├── Hosted Zones
   │
   ├── DNS Records
   │
   ├── Health Checks
   │
   └── Routing Policies
📋 Common DNS Records
Record	Purpose
A	Maps a name to an IPv4 address
AAAA	Maps a name to an IPv6 address
CNAME	Maps a name to another domain name
MX	Specifies mail servers
TXT	Stores text information
NS	Specifies authoritative name servers
🌐 Example DNS Flow
User
 │
 │ www.example.com
 ▼
Route 53
 │
 │ DNS Resolution
 ▼
Load Balancer
 │
 ▼
Application

Route 53 resolves the domain name according to the configured DNS records and routing policy.

🔀 Route 53 Routing Policies
1. Simple Routing

Routes traffic to a single resource or set of returned values.

2. Weighted Routing

Distributes traffic according to assigned weights.

Example:

Server A → 80%
Server B → 20%

Useful for controlled traffic distribution and testing.

3. Latency-Based Routing

Routes users to the AWS Region that provides the lowest network latency among configured resources.

4. Failover Routing

Routes traffic between primary and secondary resources based on health checks.

Primary
   │
Healthy?
 │     │
Yes    No
 │      │
 ▼      ▼
Serve  Secondary
5. Geolocation Routing

Routes users based on their geographic location.

6. Geoproximity Routing

Routes traffic based on geographic location and configured resource bias.

7. Multivalue Answer Routing

Returns multiple healthy resource values for a DNS query.
