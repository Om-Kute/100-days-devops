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
🔥 Why Use Terraform?
1. Automation
Terraform automates infrastructure provisioning.
Terraform Code
      ↓
Automatic Provisioning
      ↓
Infrastructure
2. Consistency
The same configuration can be used to create consistent environments.
Terraform Code
     ↓
 ┌───┼────┐
 ↓   ↓    ↓
Dev Test  Prod
3. Version Control
Terraform files can be stored in Git.
Terraform Code
      ↓
     Git
      ↓
GitHub / GitLab
This allows infrastructure changes to be reviewed and tracked.
4. Repeatability
The same Terraform configuration can be used repeatedly.
For example:
Development
     ↓
Testing
     ↓
Staging
     ↓
Production
5. Multi-Cloud
Terraform supports many providers.
Examples include:
AWS
Azure
Google Cloud
Kubernetes
GitHub
Docker
This allows Terraform to manage infrastructure across different platforms.
6. Plan Before Apply
Terraform can show proposed changes before making them.
terraform plan
This makes infrastructure changes easier to review.
🏛️ Terraform Architecture
A simplified Terraform architecture:
Terraform Configuration
                         │
                         ↓
                  ┌─────────────┐
                  │ Terraform   │
                  │     CLI     │
                  └──────┬──────┘
                         │
                    Terraform Core
                         │
             ┌───────────┼───────────┐
             ↓           ↓           ↓
           AWS         Azure        GCP
        Provider      Provider     Provider
             │           │           │
             ↓           ↓           ↓
        Infrastructure Resources
Terraform uses providers to communicate with external platforms and services.
🧩 Key Terraform Components
1. Configuration Files
Terraform configurations normally use the .tf extension.
Example:
main.tf
variables.tf
outputs.tf
providers.tf
These files contain the infrastructure configuration.
2. HCL
Terraform commonly uses HCL — HashiCorp Configuration Language.
Example:
resource "aws_instance" "web" {
  instance_type = "t2.micro"

  tags = {
    Name = "WebServer"
  }
}
HCL is designed to be:
Human readable
Declarative
Structured
Reusable
3. Providers
Providers allow Terraform to communicate with APIs and platforms.
Example AWS provider:
provider "aws" {
  region = "ap-south-1"
}
Examples of provider categories:
AWS
Azure
Google Cloud
Kubernetes
GitHub
Docker
4. Resources
Resources represent infrastructure components managed by Terraform.
Examples:
EC2 Instance
S3 Bucket
VPC
Security Group
Load Balancer
Database
Kubernetes Deployment
Example:
resource "aws_instance" "web" {
  ami           = "YOUR_AMI_ID"
  instance_type = "t2.micro"
}
5. State
Terraform maintains information about infrastructure in a state.
The default local state file is:
terraform.tfstate
Conceptually:
Terraform Configuration
        ↓
Terraform State
        ↓
Real Infrastructure
Terraform uses state to understand which real-world resources correspond to the configuration.
⚠️ State can contain sensitive information depending on the resources being managed. Protect it appropriately.
6. Modules
Terraform modules allow infrastructure code to be organized into reusable components.
Example:
Terraform Project
│
├── modules/
│   ├── vpc/
│   ├── ec2/
│   └── security-group/
│
└── main.tf
Modules are especially useful for larger infrastructure projects.
📝 Declarative Infrastructure
Terraform follows a declarative approach.
Instead of describing every individual step required to create infrastructure, we describe the desired end state.
Imperative Thinking
1. Create network
2. Create subnet
3. Create security group
4. Create server
5. Configure server
Declarative Thinking
"I want this infrastructure to exist."
              ↓
          Terraform
              ↓
    Determines required changes
🔄 Terraform Workflow
The basic Terraform workflow is:
Write
          ↓
      terraform init
          ↓
     terraform validate
          ↓
       terraform plan
          ↓
      terraform apply
          ↓
     Infrastructure
          ↓
     terraform destroy
🛠️ Important Terraform Commands
Initialize
terraform init
Initializes the working directory and downloads required provider plugins.
Validate
terraform validate
Checks whether the configuration is valid.
Format
terraform fmt
Formats Terraform configuration files.
Plan
terraform plan
Shows the changes Terraform intends to make.
Apply
terraform apply
Creates or updates infrastructure according to the configuration.
Destroy
terraform destroy
Removes infrastructure managed by the configuration.
⚠️ Use terraform destroy carefully, especially with production infrastructure.
☁️ Terraform + AWS
Terraform can be used to manage AWS infrastructure.
Example architecture:
Terraform
                     │
                     ↓
               AWS Provider
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
       EC2          VPC           S3
        │            │            │
        └────────────┼────────────┘
                     ↓
             AWS Infrastructure
🖥️ Basic AWS EC2 Example
Example Terraform configuration:
provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "example" {
  ami           = "YOUR_AMI_ID"
  instance_type = "t2.micro"

  tags = {
    Name = "Terraform-EC2"
  }
}
Important
The AMI ID must be valid for the selected AWS region.
Do not blindly copy an AMI ID from another region.
📁 Basic Terraform Project Structure
A simple project can look like:
terraform-project/
│
├── main.tf
├── providers.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
└── .gitignore
As projects become larger, modules can be introduced:
terraform-project/
│
├── main.tf
├── providers.tf
├── variables.tf
├── outputs.tf
│
├── modules/
│   ├── network/
│   ├── compute/
│   └── security/
│
└── .gitignore
🔐 Terraform Security
Infrastructure code can interact with highly privileged cloud resources.
Important security practices:
❌ Never hardcode credentials
Avoid:
provider "aws" {
  access_key = "MY_ACCESS_KEY"
  secret_key = "MY_SECRET_KEY"
}
✅ Use secure authentication
Prefer mechanisms such as:
IAM roles
AWS CLI credential configuration
Short-lived credentials
Environment-based authentication
Workload identity mechanisms where appropriate
🔒 Protect Terraform State
Do not blindly commit:
terraform.tfstate
terraform.tfstate.backup
to a public Git repository.
A useful .gitignore can contain:
.terraform/
*.tfstate
*.tfstate.*
*.tfplan
crash.log
crash.*.log
For team environments, Terraform state should generally be stored in a properly secured remote backend with appropriate access control and state-locking capabilities.
🌍 Real-World Terraform Use Cases
Terraform can be used for:
☁️ Cloud Infrastructure
EC2
VPC
S3
RDS
Load Balancers
IAM
☸️ Kubernetes
EKS
AKS
GKE
Kubernetes Resources
🔄 CI/CD
Terraform can be integrated with:
Jenkins
GitHub Actions
GitLab CI/CD
Azure DevOps
Example:
Developer
    ↓
GitHub
    ↓
CI/CD Pipeline
    ↓
Terraform Plan
    ↓
Approval
    ↓
Terraform Apply
    ↓
Cloud Infrastructure
🏢 Real-World DevOps Architecture
Terraform can become part of a complete DevOps ecosystem:
Developer
                         │
                         ↓
                      GitHub
                         │
                         ↓
                      Jenkins
                         │
             ┌───────────┴───────────┐
             ↓                       ↓
          Docker                 Terraform
             ↓                       ↓
      Container Registry        AWS Infrastructure
             ↓                       ↓
         Kubernetes             VPC / EC2 / S3
             │                       │
             └───────────┬───────────┘
                         ↓
                 Prometheus/Grafana
                         ↓
                    Monitoring
