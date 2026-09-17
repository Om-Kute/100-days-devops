🚀 Day 84/100 – Terraform State & State Management
📌 Overview
On Day 84 of my 100 Days of DevOps journey, I explored one of the most important Terraform concepts — Terraform State.
Terraform State allows Terraform to keep track of the relationship between the Terraform configuration and the real infrastructure deployed in the cloud.
The basic relationship is:
Terraform Configuration
        ↓
   Terraform State
        ↓
 Real Infrastructure
State is essential because Terraform uses it to determine what resources already exist and what changes need to be made.
🧠 What is Terraform State?
Terraform State is the record Terraform uses to track resources it manages.
The default local state file is:
terraform.tfstate
For example:
main.tf
   ↓
Terraform
   ↓
terraform.tfstate
   ↓
AWS EC2
Terraform uses state to map configuration objects to real infrastructure resources.
🔍 Why Does Terraform Need State?
Terraform needs state to understand the current infrastructure and determine what changes are required.
Suppose we have:
resource "aws_instance" "web" {
  instance_type = "t2.micro"
}
Terraform creates an EC2 instance and records information about that resource in its state.
Later, if the configuration changes:
resource "aws_instance" "web" {
  instance_type = "t3.micro"
}
Terraform can compare the configuration and state with the real infrastructure to determine the required change.
Conceptually:
Current Configuration
        ↓
Terraform State
        ↓
Real Infrastructure
        ↓
Calculate Difference
        ↓
Proposed Changes
🏗️ Terraform State Architecture
Terraform Code
                         │
                         ↓
                  ┌─────────────┐
                  │ Terraform   │
                  │    Core     │
                  └──────┬──────┘
                         │
                         ↓
                 Terraform State
                         │
              ┌──────────┴──────────┐
              ↓                     ↓
        Local State             Remote State
              │                     │
       terraform.tfstate       S3 / Backend
                                    │
                                    ↓
                              Team Collaboration
💻 Local State
By default, Terraform stores state locally.
Example:
terraform-project/
│
├── main.tf
├── variables.tf
├── outputs.tf
└── terraform.tfstate
Advantages
Simple
Easy for learning
No additional backend required
Useful for small personal experiments
Disadvantages
Difficult for teams
Risk of accidental deletion
Difficult to share
No centralized access control
Collaboration can become problematic
