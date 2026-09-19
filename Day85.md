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
💡 Why Use Modules?
1. Reusability
Write infrastructure once and reuse it.
EC2 Module
                 │
       ┌─────────┼─────────┐
       ↓         ↓         ↓
      Dev      Staging     Prod
2. Consistency
Modules help ensure that infrastructure is created using a standard configuration.
For example, an organization can create a standard EC2 module containing:
Instance configuration
Tags
Monitoring settings
Security requirements
Naming conventions
3. Maintainability
Instead of managing hundreds of lines in one file:
main.tf
 └── 1000+ lines
we can organize infrastructure:
modules/
├── vpc/
├── ec2/
├── security-group/
└── s3/
4. Scalability
Modules make it easier to manage larger infrastructure environments.
Terraform
   ↓
Modules
   ↓
Reusable Components
   ↓
Multiple Environments
   ↓
Large Infrastructure
5. DRY Principle
Modules help follow:
DRY – Don't Repeat Yourself
Instead of copying the same resource configuration multiple times, create a reusable module.
🏗️ Terraform Module Architecture
Root Module
                        │
             ┌──────────┼──────────┐
             ↓          ↓          ↓
          VPC Module  EC2 Module  S3 Module
             │          │          │
             ↓          ↓          ↓
          VPC         EC2          S3
The root module calls child modules and passes required input values.
📦 Types of Terraform Modules
There are several ways modules are commonly used.
1. Root Module
The directory where Terraform commands are executed is the root module.
Example:
terraform-project/
├── main.tf
├── variables.tf
└── outputs.tf
2. Child Module
A child module is a reusable module called by another module.
Example:
terraform-project/
│
├── main.tf
│
└── modules/
    └── ec2/
        ├── main.tf
        ├── variables.tf
        └── outputs.tf
3. Registry Module
Terraform modules can also be published and consumed from the Terraform Registry.
Example concept:
module "vpc" {
  source = "terraform-aws-modules/vpc/aws"
}
Always review a third-party module's source, version, permissions, and behavior before using it.
