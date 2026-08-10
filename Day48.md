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
🚨 3. CloudWatch Alarms
CloudWatch Alarms monitor metrics against configured thresholds.
Example:
EC2 CPU Utilization
        │
        ▼
   CPU > 70%
        │
        ▼
CloudWatch Alarm
        │
   ┌────┴─────┐
   ▼          ▼
SNS        Auto Scaling
Possible actions include:
SNS notifications
Auto Scaling actions
Other supported integrations
📊 4. CloudWatch Dashboards
Dashboards provide a centralized view of operational metrics.
They can include:
Line charts
Number widgets
Bar charts
Alarm status
Other supported widgets
Example:
┌─────────────────────────────┐
│       AWS Dashboard         │
├──────────────┬──────────────┤
│ EC2 CPU      │ Network      │
│    45%       │    2 MB/s    │
├──────────────┼──────────────┤
│ RDS          │ ALB          │
│ Connections  │ Requests     │
└──────────────┴──────────────┘
🔐 AWS CloudTrail
AWS CloudTrail provides logging and auditing of AWS API activity and account activity.
It helps answer questions such as:
Who made the API call?
What action was performed?
When did it happen?
Which AWS service was involved?
Which resource was affected?
From where did the request originate?
📝 CloudTrail Event
A CloudTrail event can contain information such as:
Event Time
User Identity
Event Source
Event Name
AWS Region
Source IP Address
User Agent
Request Parameters
Response Elements
Example event names:
RunInstances
StopInstances
CreateBucket
DeleteBucket
CreateUser
