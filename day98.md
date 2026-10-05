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
🛠️ Technology Stack

Category

Technology

Operating System

Linux

Version Control

Git

Repository

GitHub

Containerization

Docker

CI/CD

Jenkins / GitHub Actions

Infrastructure as Code

Terraform

Orchestration

Kubernetes

Cloud

AWS

Kubernetes Service

Amazon EKS

Load Balancing

AWS Load Balancer

Monitoring

Prometheus

Visualization

Grafana

Alerting

Alertmanager

Code Security

SonarQube

Container Security

Trivy

IaC Security

Checkov

Web Server

Nginx

Database

MySQL / PostgreSQL / RDS
📁 Recommended Project Structure

devops-3-tier-project/
│
├── frontend/
│   ├── Dockerfile
│   ├── src/
│   └── package.json
│
├── backend/
│   ├── Dockerfile
│   ├── src/
│   └── package.json
│
├── k8s/
│   ├── namespace.yaml
│   ├── frontend-deployment.yaml
│   ├── frontend-service.yaml
│   ├── backend-deployment.yaml
│   ├── backend-service.yaml
│   ├── configmap.yaml
│   ├── secret.yaml
│   ├── ingress.yaml
│   └── hpa.yaml
│
├── terraform/
│   ├── main.tf
│   ├── providers.tf
│   ├── variables.tf
│   ├── outputs.tf
│   ├── versions.tf
│   ├── backend.tf
│   └── modules/
│
├── monitoring/
│   ├── prometheus/
│   ├── grafana/
│   └── alertmanager/
│
├── security/
│   ├── sonar-project.properties
│   └── checkov/
│
├── Jenkinsfile
├── .gitignore
└── README.md
🔄 Complete DevOps Workflow

Developer
    │
    │ Git Push
    ▼
GitHub
    │
    ▼
CI/CD Pipeline
    │
    ├── Build
    ├── Unit Test
    ├── SAST
    ├── Dependency Scan
    ├── Docker Build
    ├── Container Scan
    ├── Push Image
    └── Deploy
             │
             ▼
        Kubernetes / EKS
             │
       ┌─────┴─────┐
       ▼           ▼
   Frontend      Backend
                     │
                     ▼
                  Database
                     │
                     ▼
                 Monitoring
                     │
             ┌───────┴────────┐
             ▼                ▼
          Prometheus        Grafana
             │
             ▼
        Alertmanager
🔀 1. Git & GitHub

Git is used to manage source-code versions.

Initialize the repository:

git init

Add remote repository:

git remote add origin https://github.com/your-username/devops-3-tier-project.git

Create a branch:

git checkout -b feature/application

Add files:

git add .

Commit:

git commit -m "Add application components"

Push:

git push origin feature/application

Create a Pull Request and review changes before merging into the protected main branch.

🐳 2. Docker Containerization

Both frontend and backend applications can be packaged as Docker images.

Example Dockerfile

FROM node:22-alpine

WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . .

EXPOSE 3000

CMD ["npm", "start"]

Build the image:

docker build -t myapp-backend:latest .

Run locally:

docker run -p 3000:3000 myapp-backend:latest

Check running containers:

docker ps
🔐 Docker Best Practices

✅ Use minimal trusted base images
✅ Use multi-stage builds where appropriate
✅ Avoid running applications as root
✅ Do not store secrets in images
✅ Scan images for vulnerabilities
✅ Pin important dependency versions
✅ Remove unnecessary packages

🏗️ 3. Infrastructure as Code with Terraform

Terraform is used to provision AWS infrastructure.

Potential resources include:

VPC
 ├── Subnets
 ├── Route Tables
 ├── Internet Gateway
 ├── NAT Gateway
 └── Security Groups

EKS
 ├── Cluster
 ├── Node Groups
 └── IAM Roles

RDS
 └── Database

Load Balancer
 └── Application Traffic
⚙️ Terraform Workflow

Initialize:

terraform init

Format:

terraform fmt -recursive

Validate:

terraform validate

Create plan:

terraform plan

Apply:

terraform apply

Destroy when the lab is no longer required:

terraform destroy

Always review terraform plan and be especially careful with terraform destroy in shared or production environments.
☸️ 4. Kubernetes Deployment

The application is deployed using Kubernetes.

Example frontend deployment:

apiVersion: apps/v1
kind: Deployment

metadata:
  name: frontend

spec:
  replicas: 3

  selector:
    matchLabels:
      app: frontend

  template:
    metadata:
      labels:
        app: frontend

    spec:
      containers:
        - name: frontend
          image: your-registry/frontend:latest

          ports:
            - containerPort: 80
🌐 Kubernetes Service

Example:

apiVersion: v1
kind: Service

metadata:
  name: frontend-service

spec:
  selector:
    app: frontend

  ports:
    - port: 80
      targetPort: 80

  type: ClusterIP

An Ingress or AWS Load Balancer integration can expose the application externally.

📈 Kubernetes Scaling

The application can use multiple replicas:

Frontend
   │
   ├── Pod 1
   ├── P🌐 Kubernetes Service

Example:

apiVersion: v1
kind: Service

metadata:
  name: frontend-service

spec:
  selector:
    app: frontend

  ports:
    - port: 80
      targetPort: 80

  type: ClusterIP

An Ingress or AWS Load Balancer integration can expose the application externally.

od 2
   └── Pod 3

Horizontal Pod Autoscaler can scale workloads based on resource utilization and other supported metrics.

Example:

apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler

metadata:
  name: frontend-hpa

spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: frontend

  minReplicas: 2
  maxReplicas: 10

  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70
