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
