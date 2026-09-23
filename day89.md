🚀 Day 89/100 – Terraform + Jenkins
📌 Overview

As part of my 100 Days of DevOps journey, Day 89 focuses on integrating Terraform with Jenkins to automate Infrastructure as Code (IaC) workflows.

Terraform is responsible for provisioning and managing infrastructure, while Jenkins automates the CI/CD workflow around Terraform.

The overall workflow can be represented as:

Developer
   │
   ▼
GitHub Repository
   │
   ▼
Jenkins CI/CD
   │
   ├── Terraform Init
   ├── Terraform Format Check
   ├── Terraform Validate
   ├── Terraform Plan
   ├── Manual Approval
   └── Terraform Apply
            │
            ▼
      AWS Infrastructure
🏗️ 1. What is Terraform?

Terraform is an Infrastructure as Code tool developed by HashiCorp.

It allows infrastructure to be defined using configuration files instead of creating cloud resources manually.

For example:

resource "aws_s3_bucket" "demo" {
  bucket = "my-demo-terraform-bucket"
}

Terraform can manage resources such as:

EC2
S3
VPC
Subnets
Security Groups
IAM
Load Balancers
RDS
Kubernetes resources
