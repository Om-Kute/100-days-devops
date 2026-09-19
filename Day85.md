🚀 Day 85/100 – Terraform Modules
📌 Overview
On Day 85 of my 100 Days of DevOps journey, I learned about Terraform Modules and how they help build reusable, maintainable, consistent, and scalable Infrastructure as Code.
As Terraform projects grow, keeping everything inside a single main.tf file can become difficult to manage. Modules allow us to organize infrastructure into reusable components.
The basic idea is:
Write Once
    ↓
Create Module
    ↓
Reuse Module
    ↓
Multiple Environments
    ↓
Standardized Infrastructure
🧩 What is a Terraform Module?
A Terraform module is a collection of Terraform configuration files that are grouped together to manage a particular part of infrastructure.
For example:
VPC Module
EC2 Module
Security Group Module
S3 Module
RDS Module
Instead of repeating the same infrastructure code, we can create a module once and reuse it.
