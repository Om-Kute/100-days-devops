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
