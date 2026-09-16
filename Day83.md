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
