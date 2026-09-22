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
