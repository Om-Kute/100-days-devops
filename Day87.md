🚀 Day 87/100 – Terraform Workspaces
📌 Overview
On Day 87 of my 100 Days of DevOps journey, I learned about Terraform Workspaces and how they can be used to manage multiple infrastructure environments with separate Terraform state.
Terraform workspaces allow the same Terraform configuration to be used with different state instances.
A simplified concept is:
Same Terraform Code
                           │
              ┌────────────┼────────────┐
              ↓            ↓            ↓
             Dev        Staging        Prod
              │            │            │
              ↓            ↓            ↓
         Separate       Separate      Separate
           State          State         State
This can be useful when similar infrastructure needs to be managed across multiple environments.
🧠 What is a Terraform Workspace?
A Terraform workspace provides a separate state for a Terraform configuration.
The same configuration can be used with multiple workspaces:
Terraform Code
      │
      ├── dev
      │     └── Separate State
      │
      ├── staging
      │     └── Separate State
      │
      └── prod
            └── Separate State
For example:
dev
staging
prod
can represent different environments.
⭐ Default Workspace
When Terraform initializes a new project, Terraform starts with a workspace named:
default
Check the current workspace:
terraform workspace show
Expected:
default
List available workspaces:
terraform workspace list
Example:
* default
The * indicates the currently selected workspace.
🔄 Why Use Workspaces?
Workspaces can be useful when the same Terraform configuration needs multiple isolated state instances.
Example:
Terraform Code
                       │
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
       Dev           Staging         Prod
        │              │              │
   Dev State      Staging State    Prod State
Potential benefits include:
Reusing the same configuration
Separating state
Managing similar environments
Reducing unnecessary code duplication
Simplifying certain development workflows
🧩 Terraform Workspace Commands
Command
Purpose
terraform workspace list
List workspaces
terraform workspace show
Show current workspace
terraform workspace new <name>
Create and select a workspace
terraform workspace select <name>
Switch workspace
terraform workspace delete <name>
Delete a workspace
1️⃣ List Workspaces
Run:
terraform workspace list
Example:
* default
After creating more workspaces:
* dev
  staging
  prod
2️⃣ Show Current Workspace
Run:
terraform workspace show
Example:
dev
This tells you which workspace is currently selected.
3️⃣ Create a Workspace
Create a development workspace:
terraform workspace new dev
Terraform creates the workspace and selects it.
Create staging:
terraform workspace new staging
Create production:
terraform workspace new prod
List them:
terraform workspace list
Example:
default
* dev
  staging
  prod
4️⃣ Select a Workspace
Switch to development:
terraform workspace select dev
Switch to staging:
terraform workspace select staging
Switch to production:
terraform workspace select prod
Verify:
terraform workspace show
5️⃣ Delete a Workspace
To delete a workspace:
terraform workspace delete dev
Terraform will normally prevent deletion if the workspace still has managed resources unless you explicitly force deletion.
⚠️ Deleting a workspace is potentially destructive. Always understand what infrastructure and state are associated with the workspace before removing it.
🏗️ Workspace Architecture
Terraform
                             │
                     Same Configuration
                             │
          ┌──────────────────┼──────────────────┐
          ↓                  ↓                  ↓
        Dev                Staging             Prod
          │                  │                  │
          ↓                  ↓                  ↓
     Dev State          Staging State       Prod State
          │                  │                  │
          ↓                  ↓                  ↓
     Dev AWS             Staging AWS          Prod AWS
The key concept is state isolation, not automatically separate cloud accounts, networks, or permissions.
💻 Using terraform.workspace
Terraform provides the built-in value:
terraform.workspace
It returns the name of the currently selected workspace.
Example:
resource "aws_instance" "web" {
  ami           = var.ami_id
  instance_type = var.instance_type

  tags = {
    Name        = "Web-${terraform.workspace}"
    Environment = terraform.workspace
  }
}
If the workspace is:
dev
the environment tag can become:
Environment = "dev"
If the workspace is:
prod
it can become:
Environment = "prod"
