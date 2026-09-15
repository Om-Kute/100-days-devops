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
