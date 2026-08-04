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
