🚀 Day 82/100 – Terraform Installation & Setup
📌 Overview
On Day 82 of my 100 Days of DevOps journey, I moved from Terraform fundamentals to hands-on installation and configuration.
Today I learned how to:
Install Terraform on Ubuntu
Verify the Terraform installation
Understand the Terraform CLI
Configure AWS credentials
Configure the AWS provider
Create a basic Terraform project
Initialize a Terraform working directory
Validate Terraform configuration
Preview infrastructure changes
Apply infrastructure changes
Destroy test infrastructure safely
🏗️ Prerequisites
Before installing Terraform, I prepared:
Ubuntu/Linux system
Terminal access
sudo privileges
Internet connectivity
AWS account for AWS-based practice
AWS CLI
IAM identity with appropriate permissions
Text editor such as VS Code, Vim, or Nano
⚠️ For production environments, use an appropriate IAM role or other short-lived/managed authentication mechanism where possible instead of long-lived access keys.
🛠️ Installing Terraform on Ubuntu
HashiCorp provides official packages for Ubuntu.
Step 1 – Update Packages
sudo apt update
sudo apt upgrade -y
Step 2 – Install Required Packages
sudo apt install -y gnupg software-properties-common
Step 3 – Add HashiCorp GPG Key
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
Step 4 – Add HashiCorp Repository
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(. /etc/os-release && echo $VERSION_CODENAME) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
Step 5 – Install Terraform
sudo apt update
sudo apt install terraform
✅ Verify Terraform Installation
Run:
terraform version
Example:
Terraform v1.x.x
on linux_amd64
The exact version will depend on the version installed on the system.
Another useful command:
terraform -help
🧰 Terraform CLI
Some important Terraform commands:
Command
Purpose
terraform version
Display Terraform version
terraform init
Initialize working directory
terraform validate
Validate configuration
terraform fmt
Format Terraform files
terraform plan
Preview changes
terraform apply
Create/update infrastructure
terraform destroy
Destroy managed infrastructure
terraform show
Display state information
terraform providers
Show configured providers
☁️ Configure AWS Credentials
Terraform needs authentication to interact with AWS.
A common learning setup is configuring the AWS CLI.
Check whether AWS CLI is installed:
aws --version
Configure credentials:
aws configure
You will be prompted for:
AWS Access Key ID
AWS Secret Access Key
Default region name
Default output format
Example region:
ap-south-1
🔐 Never commit AWS credentials to GitHub or place them directly inside .tf files.
🔎 Verify AWS Authentication
Run:
aws sts get-caller-identity
A successful response identifies the AWS principal being used.
This is a useful way to confirm that the CLI authentication is working before using Terraform.
📁 Create a Terraform Project
Create a directory:
mkdir terraform-demo
Move into it:
cd terraform-demo
Create the main configuration:
touch main.tf
Project structure:
terraform-demo/
│
├── main.tf
│
└── terraform.tfstate
terraform.tfstate is generated after Terraform manages resources. It should generally not be committed to a public Git repository.
🧩 Terraform Provider
A provider allows Terraform to interact with an external platform or service.
For AWS:
provider "aws" {
  region = "ap-south-1"
}
Terraform can use providers for platforms and services such as:
AWS
Azure
Google Cloud
Kubernetes
GitHub
Docker
🖥️ Basic AWS Terraform Configuration
Example:
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
Replace:
YOUR_AMI_ID
with an AMI that exists in the selected AWS region.
AMI IDs are region-specific, so do not blindly copy an AMI ID from another region.
🔄 Terraform Workflow
The basic Terraform workflow is:
Write
                   ↓
              .tf Files
                   ↓
                Init
                   ↓
               Validate
                   ↓
                 Plan
                   ↓
                Apply
                   ↓
              Infrastructure
                   ↓
               Destroy
1️⃣ terraform init
Initialize the Terraform working directory:
terraform init
This downloads the required provider plugins and prepares the working directory.
2️⃣ terraform validate
Validate the Terraform configuration:
terraform validate
A successful validation indicates that the configuration is syntactically and structurally valid according to Terraform's checks.
3️⃣ terraform fmt
Format Terraform configuration:
terraform fmt
Check which files would be changed:
terraform fmt -check
Formatting helps maintain consistent Terraform code.
4️⃣ terraform plan
Preview the changes Terraform intends to make:
terraform plan
This is one of the most important Terraform commands because it allows us to review changes before applying them.
Conceptually:
Terraform Configuration
        ↓
terraform plan
        ↓
Proposed Changes
        ↓
Review
5️⃣ terraform apply
Create or update infrastructure:
terraform apply
Terraform displays the proposed changes and normally asks for confirmation.
To automatically approve:
terraform apply -auto-approve
⚠️ Use -auto-approve carefully, especially in production.
6️⃣ terraform destroy
Remove resources managed by the Terraform configuration:
terraform destroy
Terraform shows the resources that will be removed before asking for confirmation.
For automated environments:
terraform destroy -auto-approve
⚠️ Never run terraform destroy against production infrastructure unless you fully understand the consequences.
