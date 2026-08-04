🔐 Day 42 – AWS IAM (Identity and Access Management)
🎯 Objective
Learn how AWS Identity and Access Management (IAM) controls authentication and authorization for AWS resources.
Topics covered:
IAM Users
IAM Groups
IAM Roles
IAM Policies
Authentication & Authorization
Access Keys
MFA
Policy Evaluation
Least Privilege
IAM Security Best Practices
🔐 What is AWS IAM?
AWS Identity and Access Management (IAM) is a service used to securely control access to AWS services and resources.
IAM helps answer four important questions:
WHO?
 │
 ▼
User / Role

CAN DO WHAT?
 │
 ▼
Actions / Permissions

ON WHICH RESOURCE?
 │
 ▼
EC2 / S3 / RDS / etc.

UNDER WHAT CONDITIONS?
 │
 ▼
Policy Conditions
🔑 Authentication vs Authorization
Authentication
Authentication verifies:
Who are you?
Examples:
Console password
MFA
Access credentials
Temporary security credentials
Authorization
Authorization determines:
What are you allowed to do?
Authorization is primarily controlled through IAM policies and other applicable AWS access controls.
👤 1. IAM Users
An IAM user represents an identity with long-term credentials that can be used for AWS access.
An IAM user can have:
Console access
Programmatic credentials
Permissions through policies
Group membership
For modern workloads, temporary credentials through IAM roles are generally preferred over long-term user credentials.
👥 2. IAM Groups
An IAM group is a collection of IAM users.
Example:
Developers Group
      │
      ├── Developer1
      ├── Developer2
      └── Developer3
A policy can be attached to the group:
Developers
     │
     ▼
IAM Policy
     │
     ▼
Permissions
All users in the group receive the permissions granted through that group.
🎭 3. IAM Roles
An IAM role is an AWS identity with permissions that can be assumed by trusted identities.
Unlike IAM users, roles are designed to provide temporary security credentials.
Common use cases:
EC2 accessing S3
Lambda accessing DynamoDB
Cross-account access
Federated users
Applications running on AWS
CI/CD workloade
📜 4. IAM Policies
IAM policies are JSON documents that define permissions.
A simplified example:
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::example-bucket/*"
    }
  ]
}
🧩 Important Policy Elements
Effect
Defines whether access is:
Allow
Deny
Action
Defines which API operations are affected.
Example:
s3:GetObject
Resource
Defines which AWS resources the statement applies to.
Example:
arn:aws:s3:::example-bucket/*
Condition
Optionally specifies conditions under which the policy statement applies.
🔄 User → Group → Policy Workflow
Create IAM User
       │
       ▼
Add User to Group
       │
       ▼
Attach Policy to Group
       │
       ▼
User Receives Permissions
Using groups can simplify permission management when multiple IAM users need the same permissions.
📝 Types of IAM Policies
Two important managed-policy categories are:
AWS Managed Policies
Created and maintained by AWS.
Examples include:
ReadOnlyAccess
AmazonS3ReadOnlyAccess
Customer Managed Policies
Created and managed within your AWS account.
Advantages include:
Greater control
Reusability
Custom permissions
Ability to tailor permissions to least privilege
Inline policies also exist and are embedded directly into a single identity.

🔑 Access Keys
Access keys can be used for programmatic AWS access.
They consist of:
Access Key ID
Secret Access Key
⚠️ Never put credentials in:
GitHub repositories
Application source code
Docker images
Public files
Screenshots
Public configuration files
For workloads running on AWS, prefer IAM roles and temporary credentials whenever possible.
📱 Multi-Factor Authentication (MFA)
MFA adds an additional authentication factor.
Instead of relying only on a password:
Password
   +
MFA Factor
   │
   ▼
Authentication
MFA is particularly important for privileged access and the AWS account root user.
⚖️ IAM Policy Evaluation
AWS starts from an implicit deny.
Applicable policies and controls are then evaluated.
A simplified concept:
Request
   │
   ▼
Evaluate Applicable Policies
   │
   ├──── Explicit Deny ────► DENIED
   │
   └──── Explicit Allow ───► Potentially Allowed
A key rule:
An applicable explicit Deny generally overrides an Allow.
The full AWS authorization model can also involve resource-based policies, permissions boundaries, Organizations SCPs, session policies, and other controls.
🛡️ Principle of Least Privilege
Least privilege means granting only the permissions required to perform a task.
Instead of:
Action: *
Resource: *
prefer narrowly scoped permissions whenever possible.
Example:
Allow only the required S3 actions
           │
           ▼
Only on the required bucket
