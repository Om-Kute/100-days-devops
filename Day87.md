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
