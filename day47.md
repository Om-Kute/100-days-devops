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
