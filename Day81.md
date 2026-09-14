🚀 Day 81/100 – Terraform Introduction & Infrastructure as Code (IaC)
📌 Overview
On Day 81 of my 100 Days of DevOps journey, I started learning Terraform and the concept of Infrastructure as Code (IaC).
Terraform is an open-source Infrastructure as Code tool that allows DevOps engineers to define, provision, and manage infrastructure using configuration files instead of manually creating resources through cloud consoles.
🏗️ What is Terraform?
Terraform is an Infrastructure as Code tool developed by HashiCorp.
It allows infrastructure to be defined using configuration files written in HCL (HashiCorp Configuration Language).
For example, instead of manually creating an EC2 instance from the AWS Console, we can define it in Terraform:
resource "aws_instance" "example" {
  ami           = "YOUR_AMI_ID"
  instance_type = "t2.micro"

  tags = {
    Name = "Terraform-EC2"
  }
}
Terraform then compares the configuration with the current infrastructure and determines what needs to be created, changed, or removed.
💡 What is Infrastructure as Code?
Infrastructure as Code (IaC) means managing infrastructure using code and configuration files.
Traditional Approach
Developer
    ↓
AWS Console
    ↓
Manual Configuration
    ↓
EC2
    ↓
VPC
    ↓
Security Groups
This can become difficult to reproduce and maintain.
Infrastructure as Code
Developer
    ↓
Terraform Code
    ↓
terraform plan
    ↓
terraform apply
    ↓
Cloud Infrastructure
Infrastructure becomes:
Version controlled
Repeatable
Automated
Reviewable
Consistent
Easier to reproduce
