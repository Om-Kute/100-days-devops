🚀 Day 84/100 – Terraform State & State Management
📌 Overview
On Day 84 of my 100 Days of DevOps journey, I explored one of the most important Terraform concepts — Terraform State.
Terraform State allows Terraform to keep track of the relationship between the Terraform configuration and the real infrastructure deployed in the cloud.
The basic relationship is:
Terraform Configuration
        ↓
   Terraform State
        ↓
 Real Infrastructure
State is essential because Terraform uses it to determine what resources already exist and what changes need to be made.
