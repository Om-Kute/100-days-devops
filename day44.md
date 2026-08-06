💾 Day 44 – AWS Storage Services (S3, EBS & EFS)
🎯 Objective

Learn the three core AWS storage services and understand when to use each one.

Topics Covered
Amazon S3
Amazon EBS
Amazon EFS
Storage Classes
Volume Types
Snapshots
Lifecycle Policies
S3 vs EBS vs EFS
Best Practices
🪣 Amazon S3 (Simple Storage Service)

Amazon S3 is a highly scalable object storage service used to store and retrieve any amount of data from anywhere.

Key Features
Object-based storage
Virtually unlimited scalability
99.999999999% (11 9's) durability
Versioning
Lifecycle management
Server-side encryption
Static website hosting
Common Use Cases
Static websites
Backup & Restore
Media files
Application logs
Data lakes
Archive storage
📦 S3 Storage Classes
Storage Class	Use Case
S3 Standard	Frequently accessed data
S3 Standard-IA	Infrequently accessed data
S3 One Zone-IA	Lower-cost infrequent access in one AZ
S3 Glacier Instant Retrieval	Archive with millisecond retrieval
S3 Glacier Flexible Retrieval	Archive with retrieval in minutes to hours
S3 Glacier Deep Archive	Long-term archive at the lowest cost
💽 Amazon EBS (Elastic Block Store)

Amazon EBS provides persistent block storage for EC2 instances.

Key Features
Block-level storage
Persistent volumes
SSD and HDD options
Low latency
Snapshots
Encryption
Boot volumes
Common Use Cases
Operating system disks
Databases
Enterprise applications
Transactional workloads
📀 Common EBS Volume Types
Volume Type	Best For
gp3	General-purpose SSD
gp2	Previous generation SSD
io2	High-performance databases
io2 Block Express	Mission-critical workloads
st1	Throughput-intensive HDD
sc1	Cold HDD
