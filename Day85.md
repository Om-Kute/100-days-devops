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
📁 Module Directory Structure
A simple project can look like:
terraform-project/
│
├── main.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
│
└── modules/
    │
    └── ec2/
        ├── main.tf
        ├── variables.tf
        └── outputs.tf
🧱 Creating a Simple EC2 Module
Let's create a reusable EC2 module.
Step 1 – Create Directory
mkdir -p modules/ec2
Project structure:
terraform-project/
│
├── main.tf
├── variables.tf
├── outputs.tf
│
└── modules/
    └── ec2/
        ├── main.tf
        ├── variables.tf
        └── outputs.tf
📝 Module main.tf
Inside:
modules/ec2/main.tf
Add:
resource "aws_instance" "this" {
  ami           = var.ami_id
  instance_type = var.instance_type

  tags = {
    Name = var.name
  }
}
The module does not hardcode the AMI or instance type.
Instead, these values are provided through variables.
🔢 Module Variables
Create:
modules/ec2/variables.tf
Example:
variable "ami_id" {
  description = "AMI ID for EC2"
  type        = string
}

variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t2.micro"
}

variable "name" {
  description = "Name tag for EC2"
  type        = string
}
Now the same module can be reused with different values.
📤 Module Outputs
Create:
modules/ec2/outputs.tf
Example:
output "instance_id" {
  description = "ID of the EC2 instance"
  value       = aws_instance.this.id
}

output "public_ip" {
  description = "Public IP of the EC2 instance"
  value       = aws_instance.this.public_ip
}
The module exposes useful values to the root module.
🌳 Root Module
Now the root module can call the EC2 module.
Example main.tf:
provider "aws" {
  region = "ap-south-1"
}

module "web_server" {
  source = "./modules/ec2"

  ami_id        = "YOUR_AMI_ID"
  instance_type = "t2.micro"
  name          = "Terraform-Web"
}
🔄 Module Data Flow
Root Module
     │
     │ Input Variables
     ↓
EC2 Module
     │
     ↓
AWS EC2
     │
     │ Outputs
     ↓
Root Module
📤 Using Module Outputs
The root module can expose the child module's outputs.
Example:
output "instance_id" {
  value = module.web_server.instance_id
}

output "public_ip" {
  value = module.web_server.public_ip
}
Then:
terraform output
can display the values.
🌍 Module Sources
Terraform supports different module sources.
1. Local Module
module "ec2" {
  source = "./modules/ec2"
}
Useful when the module exists in the same repository.
2. Git Repository
module "ec2" {
  source = "git::https://github.com/example/terraform-ec2-module.git"
}
For production, pin modules to a reviewed commit, tag, or release where appropriate.
3. Terraform Registry
Example:
module "vpc" {
  source = "terraform-aws-modules/vpc/aws"
}
A version constraint can be used:
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "~> 5.0"
}
Review module documentation and version compatibility before adoption.
4. HTTP/HTTPS Source
Terraform can also load modules from supported HTTP/HTTPS sources.
Example:
module "example" {
  source = "https://example.com/module.zip"
}
Only use trusted sources.
🔢 Module Inputs
Inputs allow a module to receive values from the caller.
Example:
module "web_server" {
  source = "./modules/ec2"

  ami_id        = "YOUR_AMI_ID"
  instance_type = "t2.micro"
  name          = "Web-Server"
}
The module receives:
ami_id
instance_type
name
📤 Module Outputs
Outputs allow a module to expose information.
Example:
output "instance_id" {
  value = aws_instance.this.id
}
The root module can access it:
module.web_server.instance_id
🔄 Complete Module Flow
Root Module
                      │
                      │ Inputs
                      ↓
                ┌───────────┐
                │ EC2 Module│
                └─────┬─────┘
                      │
                      ↓
                  AWS EC2
                      │
                      │ Outputs
                      ↓
                  Root Module
