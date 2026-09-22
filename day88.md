🚀 Day 88/100 – Terraform + GitHub
📌 Overview

On Day 88 of my 100 Days of DevOps journey, I explored how Terraform Infrastructure as Code (IaC) can be integrated with Git and GitHub.

Terraform files are code, so they can be managed using the same version-control practices used for application development:

Terraform Code
      ↓
     Git
      ↓
   GitHub
      ↓
Pull Request
      ↓
Code Review
      ↓
Terraform Validation
      ↓
Terraform Plan
      ↓
Approval
      ↓
Infrastructure Deployment

This approach helps teams track infrastructure changes, review them before deployment, collaborate safely, and maintain an audit trail of infrastructure code.
🧠 Why Use GitHub with Terraform?

Terraform manages infrastructure, but GitHub manages the source code that defines that infrastructure.

Without version control:

Terraform Files
      ↓
Manual Changes
      ↓
Hard to Track
      ↓
Hard to Review
      ↓
Higher Risk

With GitHub:

Terraform Files
      ↓
Git
      ↓
GitHub
      ↓
Pull Request
      ↓
Code Review
      ↓
Approved Change
      ↓
CI/CD
🔥 Benefits
1. Version Control

Every Terraform configuration change can be tracked.

Example:

Commit 1 → Create VPC
Commit 2 → Add Subnet
Commit 3 → Add Security Group
Commit 4 → Update EC2
2. Collaboration

Multiple DevOps engineers can work on infrastructure code using branches and Pull Requests.

3. Code Review

Terraform changes can be reviewed before they affect real infrastructure.

4. Auditability

Git history provides information about:

What changed
When it changed
Which commit changed it
Which branch contained the change
5. CI/CD Integration

Terraform can be integrated with CI/CD systems to automatically run:

terraform fmt
terraform validate
terraform plan

before changes are applied.
📁 Recommended Terraform + GitHub Repository Structure

A simple project:

terraform-project/
│
├── main.tf
├── providers.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars.example
├── versions.tf
├── .gitignore
└── README.md

A larger project:

terraform-project/
│
├── environments/
│   ├── dev/
│   ├── staging/
│   └── prod/
│
├── modules/
│   ├── vpc/
│   ├── ec2/
│   ├── security-group/
│   └── s3/
│
├── main.tf
├── providers.tf
├── variables.tf
├── outputs.tf
├── versions.tf
├── .gitignore
└── README.md
🔐 Terraform .gitignore

Terraform generates files that should generally not be committed to Git.

Example .gitignore:

# Terraform working directory
.terraform/

# Terraform state
*.tfstate
*.tfstate.*

# Terraform plan files
*.tfplan

# Crash logs
crash.log
crash.*.log

# Local variable files that may contain secrets
*.tfvars
*.tfvars.json

# Override files
override.tf
override.tf.json
*_override.tf
*_override.tf.json

If a .tfvars file contains no sensitive information and is intentionally meant to be shared, it can be committed selectively. A safer pattern is usually to commit a terraform.tfvars.example file instead.
🚨 Never Commit Secrets

Never commit:

AWS Access Keys
AWS Secret Keys
Passwords
API Tokens
Private Keys
Kubeconfig Secrets
Database Credentials
Terraform State

Example of what NOT to do:

provider "aws" {
  access_key = "AKIAxxxxxxxx"
  secret_key = "xxxxxxxx"
}

Instead, use secure authentication mechanisms such as:

IAM roles
AWS CLI credential configuration
Environment-based credentials
Short-lived credentials
CI/CD identity mechanisms
📄 Example terraform.tfvars.example

Instead of committing a real secrets file:

terraform.tfvars

create:

terraform.tfvars.example

Example:

aws_region   = "ap-south-1"
instance_type = "t2.micro"
environment   = "dev"

The actual terraform.tfvars can remain local or be supplied securely through the CI/CD environment.
🌿 Git Branching Strategy

A basic workflow:

main
 │
 ├── feature/vpc
 │
 ├── feature/ec2
 │
 └── feature/security-group

Example:

git checkout -b feature/vpc

Make changes:

git add .
git commit -m "Add VPC configuration"

Push:

git push -u origin feature/vpc

Then create a Pull Request on GitHub.
🔄 Terraform + GitHub Workflow
              Developer
                  │
                  ↓
          Modify Terraform
                  │
                  ↓
              Git Branch
                  │
                  ↓
              Git Commit
                  │
                  ↓
             GitHub Push
                  │
                  ↓
           Pull Request
                  │
                  ↓
             Code Review
                  │
                  ↓
        ┌─────────┴─────────┐
        ↓                   ↓
terraform fmt        terraform validate
        │                   │
        └─────────┬─────────┘
                  ↓
          terraform plan
                  ↓
             Approval
                  ↓
          terraform apply
                  ↓
          Cloud Infrastructure
🧹 Terraform Formatting

Terraform code should be consistently formatted.

Run:

terraform fmt

For a complete directory tree:

terraform fmt -recursive

Check formatting without modifying files:

terraform fmt -check
✅ Terraform Validation

Run:

terraform validate

This checks whether the Terraform configuration is syntactically valid and internally consistent.

A typical workflow is:

terraform fmt
terraform validate
🔍 Terraform Plan

The next step is:

terraform plan

Terraform calculates the proposed infrastructure changes.

Conceptually:

GitHub Code
     ↓
Terraform Plan
     ↓
Proposed Changes
     ↓
Code Review
     ↓
Approval

The plan should be reviewed before applying infrastructure changes.

🚀 Terraform Apply

After appropriate review and approval:

terraform apply

Terraform applies the configuration to the target infrastructure.

In production environments, apply should normally be controlled through an appropriate approval process rather than allowing every Pull Request to directly change production.
🧪 Pull Request Workflow

A good Terraform Pull Request can follow:

1. Create Branch
        ↓
2. Modify Terraform
        ↓
3. terraform fmt
        ↓
4. terraform validate
        ↓
5. Commit Changes
        ↓
6. Push to GitHub
        ↓
7. Open Pull Request
        ↓
8. CI Validation
        ↓
9. terraform plan
        ↓
10. Review
        ↓
11. Approval
        ↓
12. Merge
🤖 CI Checks for Terraform

A CI pipeline can automatically run:

terraform fmt -check -recursive
terraform init
terraform validate
terraform plan

Example:

Pull Request
     ↓
GitHub
     ↓
CI Pipeline
     ↓
terraform fmt -check
     ↓
terraform init
     ↓
terraform validate
     ↓
terraform plan
     ↓
Status Check
🐙 GitHub Actions Example

A simple GitHub Actions workflow can run Terraform checks.

Create:

.github/workflows/terraform.yml

Example:

name: Terraform

on:
  pull_request:
  push:
    branches:
      - main

permissions:
  contents: read

jobs:
  terraform:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v3

      - name: Terraform Format Check
        run: terraform fmt -check -recursive

      - name: Terraform Init
        run: terraform init -backend=false

      - name: Terraform Validate
        run: terraform validate

This example focuses on formatting, initialization, and validation.

A real deployment pipeline should additionally handle:

Secure cloud authentication
Remote state
terraform plan
Approval
terraform apply

with appropriate permissions and environment protection.

🔐 GitHub Secrets

Sensitive credentials should not be stored directly in Terraform files.

If a CI/CD system requires secrets, use an appropriate secure secret-management mechanism.

For GitHub Actions, repository or environment secrets can be used where appropriate.

Conceptually:

GitHub
   ↓
Secure Secret
   ↓
CI/CD Runner
   ↓
Terraform
   ↓
AWS

Avoid printing secrets in workflow logs.

☁️ Terraform + AWS + GitHub

A common architecture:

                    Developer
                        │
                        ↓
                     GitHub
                        │
                 Pull Request
                        │
                        ↓
                  CI/CD Pipeline
                        │
             ┌──────────┴──────────┐
             ↓                     ↓
       Terraform fmt         Terraform validate
             │                     │
             └──────────┬──────────┘
                        ↓
                Terraform Plan
                        │
                    Approval
                        │
                        ↓
                Terraform Apply
                        │
                        ↓
                       AWS
             ┌──────────┼──────────┐
             ↓          ↓          ↓
            VPC        EC2         S3
🗄️ GitHub is NOT Terraform State

A common misconception is that GitHub should store the Terraform state file.

GitHub should normally store:

Terraform Configuration
Terraform Modules
Documentation
CI/CD Workflows

Terraform state should be stored in an appropriate backend.

Example:

GitHub
  ↓
Terraform Code

Remote Backend
  ↓
Terraform State

For AWS, an S3 backend is commonly used for remote state, with appropriate security and locking support.

🔒 State Security

Never commit:

terraform.tfstate
terraform.tfstate.backup

Terraform state may contain sensitive information depending on the resources being managed.

Use:

Remote backend
Encryption
Access controls
Least privilege
State locking where supported
Versioning/backups
Audit logging
🏗️ Environment-Based Repository Structure

A possible structure:

terraform-infrastructure/
│
├── environments/
│   ├── dev/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   │
│   ├── staging/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   │
│   └── prod/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
│
├── modules/
│   ├── vpc/
│   ├── ec2/
│   └── security-group/
│
├── .github/
│   └── workflows/
│       └── terraform.yml
│
├── .gitignore
└── README.md

This is one possible architecture; teams may choose different layouts depending on their infrastructure and isolation requirements.

🔄 Git Workflow Commands
Clone Repository
git clone <repository-url>
Create Branch
git checkout -b feature/terraform-vpc
Check Status
git status
Add Changes
git add .
Commit
git commit -m "Add Terraform VPC configuration"
Push
git push -u origin feature/terraform-vpc
