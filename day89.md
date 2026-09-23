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
