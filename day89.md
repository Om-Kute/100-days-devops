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
⚙️ 2. What is Jenkins?

Jenkins is an open-source automation server commonly used to build CI/CD pipelines.

Jenkins can automatically:

Pull code from GitHub
Run tests
Validate configurations
Execute Terraform commands
Generate Terraform plans
Request manual approval
Deploy infrastructure
Monitor pipeline results
🔗 3. Why Use Jenkins with Terraform?

Using Terraform manually for every infrastructure change can become repetitive.

Jenkins can automate the workflow.

Without Jenkins
Developer
   │
   ├── terraform init
   ├── terraform validate
   ├── terraform plan
   └── terraform apply
With Jenkins
Developer
     │
     ▼
   GitHub
     │
     ▼
   Jenkins
     │
     ├── Init
     ├── Format
     ├── Validate
     ├── Plan
     ├── Approval
     └── Apply
     │
     ▼
    AWS

This provides a more consistent and auditable deployment process.
🔄 4. Terraform + Jenkins CI/CD Workflow

A typical workflow is:

        Developer
            │
            │ git push
            ▼
        ┌─────────┐
        │ GitHub  │
        └────┬────┘
             │
             ▼
        ┌─────────┐
        │ Jenkins │
        └────┬────┘
             │
             ▼
      Terraform Init
             │
             ▼
       Terraform Fmt
             │
             ▼
      Terraform Validate
             │
             ▼
        Terraform Plan
             │
             ▼
      Manual Approval
             │
             ▼
       Terraform Apply
             │
             ▼
     AWS Infrastructure
🧰 5. Jenkins Requirements

Before creating the pipeline, Jenkins should have access to the required tools.

Required tools
Jenkins
Git
Terraform
AWS CLI (optional depending on workflow)
GitHub repository
AWS credentials
Terraform Jenkins plugin/integration where appropriate
Useful Jenkins plugins

Commonly used plugins include:

Pipeline
Git
GitHub integration
Credentials Binding
AWS Credentials
Terraform-related tooling where needed

Plugin names and installation methods can vary with the Jenkins version and environment.
