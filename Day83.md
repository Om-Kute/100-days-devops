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
🏷️ Tags with Variables
Variables can be used to create reusable tags.
variables.tf
variable "environment" {
  type    = string
  default = "dev"
}
main.tf
resource "aws_instance" "web" {
  ami           = "YOUR_AMI_ID"
  instance_type = "t2.micro"

  tags = {
    Name        = "Terraform-Web"
    Environment = var.environment
  }
}
📁 Recommended Project Structure
For a small Terraform project:
terraform-project/
│
├── main.tf
├── variables.tf
├── outputs.tf
├── providers.tf
├── terraform.tfvars
└── .gitignore
For a larger project:
terraform-project/
│
├── main.tf
├── variables.tf
├── outputs.tf
├── providers.tf
├── versions.tf
├── data.tf
│
├── environments/
│   ├── dev/
│   ├── staging/
│   └── prod/
│
├── modules/
│   ├── vpc/
│   ├── ec2/
│   └── security-group/
│
└── .gitignore
🔄 Terraform Configuration Workflow
Write HCL
   ↓
terraform fmt
   ↓
terraform init
   ↓
terraform validate
   ↓
terraform plan
   ↓
Review Changes
   ↓
terraform apply
   ↓
Infrastructure
🛠️ Important Terraform Commands
Initialize
terraform init
Initializes the Terraform working directory.
Format
terraform fmt
Formats Terraform configuration files.
Validate
terraform validate
Checks the configuration for syntax and internal consistency.
Plan
terraform plan
Shows the changes Terraform plans to make.
Apply
terraform apply
Creates or updates infrastructure.
Show Outputs
terraform output
Displays configured output values.
Show Providers
terraform providers
Displays the providers required by the configuration.
🧪 Hands-On Example – AWS EC2
providers.tf
provider "aws" {
  region = "ap-south-1"
}
variables.tf
variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t2.micro"
}

variable "environment" {
  description = "Deployment environment"
  type        = string
  default     = "dev"
}
main.tf
resource "aws_instance" "web" {
  ami           = "YOUR_AMI_ID"
  instance_type = var.instance_type

  tags = {
    Name        = "Terraform-Web"
    Environment = var.environment
  }
}
outputs.tf
output "instance_id" {
  description = "EC2 instance ID"
  value       = aws_instance.web.id
}

output "public_ip" {
  description = "EC2 public IP"
  value       = aws_instance.web.public_ip
}
▶️ Run the Configuration
Step 1 – Initialize
terraform init
Step 2 – Format
terraform fmt
Step 3 – Validate
terraform validate
Step 4 – Plan
terraform plan
Step 5 – Apply
terraform apply
Step 6 – Check Outputs
terraform output
🔐 Security Best Practices
Never Hardcode Credentials
❌ Avoid:
provider "aws" {
  access_key = "YOUR_ACCESS_KEY"
  secret_key = "YOUR_SECRET_KEY"
}
Use secure AWS authentication mechanisms instead.
Protect Sensitive Variables
If a variable contains sensitive information:
variable "database_password" {
  type      = string
  sensitive = true
}
However, marking a variable as sensitive mainly prevents casual display in Terraform CLI output; it does not make the underlying value safe to commit or store insecurely.
🚫 Git Best Practices
Avoid committing:
.terraform/
terraform.tfstate
terraform.tfstate.backup
*.tfplan
A basic .gitignore:
.terraform/
*.tfstate
*.tfstate.*
*.tfplan
crash.log
crash.*.log
If a .tfvars file contains secrets, keep it out of source control as well:
*.tfvars
💡 Configuration Best Practices
✅ Use Variables
Avoid unnecessary hardcoded values.
✅ Use Outputs
Expose important infrastructure information.
✅ Use Data Sources
Read existing infrastructure information when appropriate.
✅ Separate Configuration
Use logical files such as:
main.tf
variables.tf
outputs.tf
providers.tf
✅ Use Formatting
Run:
terraform fmt
✅ Validate Before Planning
Run:
terraform validate
✅ Review Plans
Always review:
terraform plan
before applying important infrastructure changes.
✅ Use Version Constraints
Pin or constrain Terraform/provider versions appropriately for reproducible environments.
⚠️ Common Mistakes
1. Hardcoding Values
Hardcoded configuration becomes difficult to reuse.
Better:
instance_type = var.instance_type
2. Hardcoding Credentials
Never store AWS access keys or secrets in Terraform source code.
3. Using Invalid AMI IDs
AMI IDs are region-specific.
Always verify the AMI for your selected region.
4. Ignoring Terraform State
Terraform depends heavily on state to manage infrastructure correctly.
5. Skipping terraform plan
Always understand what Terraform is going to change.
6. Committing Secrets
Never commit:
Passwords
API keys
Private keys
Cloud credentials
Sensitive tfvars
to a public repository.
