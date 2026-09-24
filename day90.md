🚀 Day 90/100 – Terraform End-to-End Project
🌍 Real-World Infrastructure Deployment with Terraform, GitHub, Jenkins & AWS

Day 90 brings together the Terraform concepts learned throughout the Infrastructure as Code section into a practical end-to-end DevOps infrastructure workflow.

The project demonstrates how infrastructure can be:

📝 Written as code
📦 Stored in GitHub
🔄 Automated through Jenkins
🏗️ Provisioned using Terraform
☁️ Deployed to AWS
🔐 Managed securely
🌎 Organized across multiple environments
📊 Maintained through a repeatable CI/CD workflow
🎯 Project Goal

The main objective is to build a production-like Infrastructure as Code workflow using:

GitHub
   ↓
Jenkins
   ↓
Terraform
   ↓
AWS

The project combines:

Terraform
+ Modules
+ Remote State
+ GitHub
+ Jenkins
+ AWS
+ CI/CD
+ Environment Management
🏗️ High-Level Architecture
                    ┌──────────────┐
                    │  Developer   │
                    │ Terraform    │
                    │    Code      │
                    └──────┬───────┘
                           │
                           │ git push
                           ▼
                    ┌──────────────┐
                    │    GitHub    │
                    │ Source Code  │
                    └──────┬───────┘
                           │
                           │ Webhook / Trigger
                           ▼
                    ┌──────────────┐
                    │   Jenkins    │
                    │    CI/CD     │
                    └──────┬───────┘
                           │
                           ▼
                 ┌──────────────────┐
                 │     Terraform    │
                 │                  │
                 │ Init             │
                 │ Format           │
                 │ Validate         │
                 │ Plan             │
                 │ Approval         │
                 │ Apply            │
                 └────────┬─────────┘
                          │
                          ▼
                   ┌──────────────┐
                   │     AWS      │
                   │Infrastructure│
                   └──────────────┘
☁️ AWS Infrastructure

The project can provision infrastructure such as:

                    AWS
                     │
        ┌────────────┼────────────┐
        │            │            │
        ▼            ▼            ▼
       VPC        Security       S3
                    Groups
        │
        ├───────────────┐
        │               │
        ▼               ▼
   Public Subnet    Private Subnet
        │               │
        ▼               ▼
       EC2             EC2
        │
        ▼
       ALB

Depending on project requirements, the infrastructure can include:

VPC
Public subnets
Private subnets
Route tables
Internet Gateway
NAT Gateway
Security Groups
EC2
Application Load Balancer
S3
IAM
CloudWatch

Resource selection should match the project requirements and AWS cost constraints.

📁 Project Structure

A recommended repository structure is:

terraform-end-to-end/
│
├── Jenkinsfile
├── README.md
├── .gitignore
│
├── backend.tf
├── providers.tf
├── versions.tf
├── variables.tf
├── outputs.tf
├── main.tf
│
├── modules/
│   │
│   ├── vpc/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   │
│   ├── security-group/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   │
│   ├── ec2/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   │
│   └── s3/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
│
└── environments/
    │
    ├── dev/
    │   ├── main.tf
    │   ├── variables.tf
    │   └── terraform.tfvars
    │
    ├── staging/
    │   ├── main.tf
    │   ├── variables.tf
    │   └── terraform.tfvars
    │
    └── prod/
        ├── main.tf
        ├── variables.tf
        └── terraform.tfvars
🧩 Terraform Modules

Modules make Terraform code reusable.

For example:

modules/
│
├── vpc/
├── ec2/
├── security-group/
└── s3/

Instead of repeatedly writing the same infrastructure code, the root configuration can call modules.

Example:

module "vpc" {
  source = "./modules/vpc"

  project_name = var.project_name
  environment  = var.environment
  vpc_cidr     = var.vpc_cidr
}

Another environment can reuse the same module:

module "vpc" {
  source = "../../modules/vpc"

  project_name = "dev-project"
  environment  = "dev"
  vpc_cidr     = "10.10.0.0/16"
}
Benefits
Reusable
   ↓
Consistent
   ↓
Maintainable
   ↓
Scalable
🔐 Remote Terraform State

Terraform state contains information about resources managed by Terraform.

For team-based and CI/CD workflows, state should generally be stored remotely instead of committing it to Git.

For AWS, an S3 backend is commonly used.

Example:

terraform {
  backend "s3" {
    bucket       = "my-terraform-state-bucket"
    key          = "project/terraform.tfstate"
    region       = "ap-south-1"
    encrypt      = true
    use_lockfile = true
  }
}
State Architecture
              Terraform
                  │
                  ▼
          ┌──────────────┐
          │      S3      │
          │ Terraform    │
          │    State     │
          └──────────────┘
State security
Enable encryption
Restrict IAM access
Enable versioning where appropriate
Enable appropriate bucket protections
Do not commit state to Git
Back up according to recovery requirements
State locking

Modern Terraform S3 backends support native state locking using the S3 backend's lock-file mechanism.

Older architectures may use DynamoDB for state locking. If using DynamoDB locking in an existing setup, follow the Terraform version and backend documentation applicable to that environment.
🌎 Environment Management

The project can separate environments:

              Terraform
                  │
       ┌──────────┼──────────┐
       ▼          ▼          ▼
      Dev       Staging      Prod
       │          │          │
       ▼          ▼          ▼
      AWS        AWS        AWS

Example:

dev
├── smaller resources
├── automatic deployment where appropriate
└── development testing

staging
├── production-like configuration
├── plan review
└── approval before deployment

prod
├── strict access control
├── protected branch
├── mandatory review
└── controlled deployment

For stronger isolation, production infrastructure should generally use appropriate separate AWS accounts, credentials, state, and access boundaries rather than relying only on workspace or directory names.

🔄 Complete CI/CD Workflow

The end-to-end pipeline:

Developer
    │
    │ Write Terraform
    ▼
GitHub
    │
    │ Push / Pull Request
    ▼
Jenkins
    │
    ├── Checkout
    │
    ├── Terraform Init
    │
    ├── Terraform Format
    │
    ├── Terraform Validate
    │
    ├── Terraform Plan
    │
    ├── Manual Approval
    │
    └── Terraform Apply
             │
             ▼
        AWS Infrastructure
⚙️ Jenkins Pipeline

A basic Jenkinsfile can look like:

pipeline {
    agent any

    tools {
        terraform 'terraform'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Format') {
            steps {
                sh 'terraform fmt -check -recursive'
            }
        }

        stage('Terraform Validate') {
            steps {
                sh 'terraform validate'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Approval') {
            steps {
                input message: 'Approve Terraform deployment?'
            }
        }

        stage('Terraform Apply') {
            steps {
                sh 'terraform apply tfplan'
            }
        }
    }
}

The exact pipeline depends on how Jenkins agents, Terraform, AWS authentication, credentials, and the repository are configured.

🔍 Pipeline Stages Explained
1. Checkout

Jenkins retrieves the latest Terraform code.

GitHub
   ↓
Jenkins Workspace
2. Terraform Init
terraform init

Initializes:

Backend
Providers
Modules
Terraform working directory
3. Terraform Format
terraform fmt -check -recursive

Checks Terraform formatting.

4. Terraform Validate
terraform validate

Checks Terraform configuration for valid syntax and internal consistency.

5. Terraform Plan
terraform plan -out=tfplan

Creates an execution plan.

Example:

Plan:

+ Create
~ Modify
- Destroy

The plan should be reviewed before production changes are applied.
🛑 6. Manual Approval

Production deployments can include an approval stage.

stage('Approval') {
    steps {
        input message: 'Approve Terraform deployment?'
    }
}

Workflow:

Terraform Plan
      │
      ▼
Review
      │
      ▼
Approval
      │
      ▼
Terraform Apply
🚀 7. Terraform Apply

After approval:

terraform apply tfplan

Using the reviewed plan helps keep the apply operation aligned with the plan that was inspected.

🏗️ Example VPC Module

Example:

resource "aws_vpc" "this" {
  cidr_block = var.vpc_cidr

  tags = {
    Name        = "${var.project_name}-${var.environment}-vpc"
    Environment = var.environment
  }
}

resource "aws_subnet" "public" {
  vpc_id                  = aws_vpc.this.id
  cidr_block              = var.public_subnet_cidr
  map_public_ip_on_launch = true

  tags = {
    Name        = "${var.project_name}-${var.environment}-public"
    Environment = var.environment
  }
}
📦 Example Variables
variable "project_name" {
  type        = string
  description = "Project name"
}

variable "environment" {
  type        = string
  description = "Deployment environment"
}

variable "vpc_cidr" {
  type        = string
  description = "VPC CIDR block"
}

variable "public_subnet_cidr" {
  type        = string
  description = "Public subnet CIDR block"
}
📤 Example Outputs
output "vpc_id" {
  description = "VPC ID"
  value       = aws_vpc.this.id
}

Outputs can be used by other modules or displayed after deployment.

terraform output
