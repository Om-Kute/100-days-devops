orld DevOps Project

🏗️ Production-Like 3-Tier Web Application on AWS

Day 98 focuses on bringing together the technologies and practices learned throughout the 100 Days of DevOps journey into a practical, real-world project.

The objective is to design and deploy a 3-Tier Web Application using AWS and Kubernetes while implementing:

🔀 Git & GitHub

🐳 Docker

⚙️ Jenkins / GitHub Actions

☸️ Kubernetes / AWS EKS

🏗️ Terraform

📊 Prometheus & Grafana

🚨 Alertmanager

🔐 DevSecOps

🔍 Security scanning

📝 Documentation

The project follows a complete DevOps lifecycle:

Plan
  ↓
Code
  ↓
Build
  ↓
Test
  ↓
Security Scan
  ↓
Containerize
  ↓
Deploy
  ↓
Monitor
  ↓
Alert
  ↓
Optimize
🏗️ Application Architecture

The project follows a 3-tier architecture:

                 INTERNET USERS
                       │
                       ▼
              ┌─────────────────┐
              │  AWS Load       │
              │  Balancer       │
              └────────┬────────┘
                       │
                       ▼
             ┌──────────────────┐
             │     FRONTEND     │
             │   React / Nginx  │
             │    Kubernetes    │
             └────────┬─────────┘
                      │
                      ▼
             ┌──────────────────┐
             │     BACKEND      │
             │ Node.js / Python │
             │    Kubernetes    │
             └────────┬─────────┘
                      │
                      ▼
             ┌──────────────────┐
             │     DATABASE     │
             │ MySQL/PostgreSQL │
             │ RDS / Kubernetes │
             └──────────────────┘
☁️ AWS Architecture

A production-like deployment can be structured as:

                         AWS
                          │
                  ┌───────┴────────┐
                  │       VPC       │
                  └───────┬────────┘
                          │
            ┌─────────────┴─────────────┐
            │                           │
            ▼                           ▼
      Public Subnets              Private Subnets
            │                           │
            ▼                           ▼
       Load Balancer                EKS Nodes
                                        │
                              ┌─────────┴─────────┐
                              │                   │
                              ▼                   ▼
                         Frontend Pods       Backend Pods
                                                   │
                                                   ▼
                                              Database
                                                   │
                                                   ▼
                                                  RDS

The exact architecture depends on project requirements, security boundaries, and AWS cost constraints.
