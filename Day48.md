📊 Day 48 – AWS CloudWatch & CloudTrail
🎯 Objective
Learn how AWS CloudWatch provides monitoring and observability while AWS CloudTrail provides API activity logging and auditing.
📊 Amazon CloudWatch
Amazon CloudWatch is an AWS monitoring and observability service used to collect and analyze metrics, logs, and other operational data.
It can help monitor:
EC2
RDS
Lambda
EBS
Application Load Balancers
Auto Scaling
Applications
📈 1. CloudWatch Metrics
Metrics are time-series measurements collected from AWS resources and applications.
Examples:
CPUUtilization
NetworkIn
NetworkOut
DiskReadOps
DiskWriteOps
For EC2, CPU utilization is a common metric used to understand workload behavior and can also be used with Auto Scaling policies.
📜 2. CloudWatch Logs
CloudWatch Logs can collect and store log data from applications and AWS resources.
Example sources:
EC2
Lambda
Applications
AWS Services
Basic flow:
Application
     │
     ▼
Log Group
     │
     ▼
Log Stream
     │
     ▼
Log Events
Logs can be searched and analyzed to troubleshoot application and infrastructure problems.
