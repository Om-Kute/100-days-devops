🚀 Day 83/100 – Terraform Configuration
📌 Overview
On Day 83 of my 100 Days of DevOps journey, I explored Terraform configuration in more depth.
I learned how Terraform uses HCL (HashiCorp Configuration Language) to define infrastructure and how important components such as Providers, Resources, Variables, Outputs, and Data Sources work together.
The goal was to understand how to write Terraform code that is:
🧩 Modular
🔄 Reusable
📖 Easy to understand
📦 Maintainable
⚙️ Scalable
🔐 Secure
🧩 What is HCL?
HCL (HashiCorp Configuration Language) is the configuration language commonly used by Terraform.
Example:
resource "aws_instance" "web" {
  instance_type = "t2.micro"

  tags = {
    Name = "Terraform-Web"
  }
}
HCL is designed to be:
Human-readable
Declarative
Structured
Easy to maintain
🏗️ Terraform Configuration Structure
A Terraform project can be organized like this:
terraform-project/
│
├── main.tf
├── providers.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
├── data.tf
├── versions.tf
└── .gitignore
File Responsibilities
File
Purpose
main.tf
Main infrastructure resources
providers.tf
Provider configuration
variables.tf
Input variables
outputs.tf
Output values
terraform.tfvars
Variable values
data.tf
Data sources
versions.tf
Terraform/provider version constraints
.gitignore
Prevent unwanted files from Git
Terraform loads all .tf files in a directory together. The filenames are mainly used to organize the configuration for humans.
☁️ Provider Configuration
A provider allows Terraform to interact with an external platform or service.
Example AWS provider:
provider "aws" {
  region = "ap-south-1"
}
Terraform can work with many providers, including:
AWS
Azure
Google Cloud
Kubernetes
GitHub
Docker
📦 Resource
A resource represents an infrastructure object that Terraform manages.
Examples:
EC2
S3
VPC
Security Group
RDS
Load Balancer
Kubernetes Deployment
Example:
resource "aws_instance" "web" {
  ami           = "YOUR_AMI_ID"
  instance_type = "t2.micro"

  tags = {
    Name = "Terraform-Web"
  }
}
Resource syntax:
resource "<RESOURCE_TYPE>" "<LOCAL_NAME>" {
    configuration
}
For example:
aws_instance → Resource type
web          → Local name
🔢 Input Variables
Variables make Terraform configurations reusable.
Instead of hardcoding values:
instance_type = "t2.micro"
we can use:
instance_type = var.instance_type
variables.tf
variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t2.micro"
}
main.tf
resource "aws_instance" "web" {
  ami           = "YOUR_AMI_ID"
  instance_type = var.instance_type

  tags = {
    Name = "Terraform-Web"
  }
}
Now the same configuration can be used with different instance types.
🎛️ Variable Types
Terraform supports several useful variable types.
String
variable "environment" {
  type    = string
  default = "dev"
}
Number
variable "instance_count" {
  type    = number
  default = 1
}
Boolean
variable "monitoring_enabled" {
  type    = bool
  default = true
}
List
variable "availability_zones" {
  type = list(string)
}
Map
variable "tags" {
  type = map(string)
}
📄 terraform.tfvars
Variable values can be provided through a .tfvars file.
Example:
instance_type = "t2.micro"
environment   = "dev"
Terraform automatically loads:
terraform.tfvars
and:
*.auto.tfvars
files.
You can also explicitly specify a variable file:
terraform plan -var-file="dev.tfvars"
📤 Outputs
Outputs expose useful information after Terraform creates infrastructure.
Example:
output "instance_id" {
  description = "ID of the EC2 instance"
  value       = aws_instance.web.id
}
Another example:
output "public_ip" {
  description = "Public IP address"
  value       = aws_instance.web.public_ip
}
After deployment:
terraform output
Example:
instance_id = "i-xxxxxxxx"
public_ip   = "xx.xx.xx.xx"
🔎 Data Sources
A data source allows Terraform to retrieve information about existing infrastructure or external data without managing that object as a resource.
For example, we can retrieve an existing AWS AMI.
Example:
data "aws_ami" "ubuntu" {
  most_recent = true

  owners = ["099720109477"]

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-*"]
  }
}
Then use it:
resource "aws_instance" "web" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = var.instance_type
}
Conceptually:
Existing AWS Information
          ↓
      Data Source
          ↓
       Terraform
          ↓
     Resource
🔄 Resource vs Data Source
Resource
Data Source
Creates/manages infrastructure
Reads existing information
Terraform controls lifecycle
Terraform does not manage the object's lifecycle
🔎 Data Sources
A data source allows Terraform to retrieve information about existing infrastructure or external data without managing that object as a resource.
For example, we can retrieve an existing AWS AMI.
Example:
data "aws_ami" "ubuntu" {
  most_recent = true

  owners = ["099720109477"]

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-*"]
  }
}
Then use it:
resource "aws_instance" "web" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = var.instance_type
}
Conceptually:
Existing AWS Information
          ↓
      Data Source
          ↓
       Terraform
          ↓
     Resource
🔄 Resource vs Data Source
Resource
Data Source
Creates/manages infrastructure
Reads existing information
Terraform controls lifecycle
Terraform does not manage the object's lifecycle
Example: create EC2
Example: find an existing AMI
Uses resource
Uses data
🧮 Terraform Expressions
Terraform supports expressions for creating dynamic configurations.
Example:
instance_type = var.environment == "prod" ? "t3.medium" : "t2.micro"
This is a conditional expression.
Another example:
name = "${var.environment}-server"
Terraform also supports:
Arithmetic expressions
Conditional expressions
String interpolation
Collection operations
Functions
for expressions
