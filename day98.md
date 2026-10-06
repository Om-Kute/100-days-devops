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
🚀 5. CI/CD Pipeline

The CI/CD pipeline automates the application delivery process.

Code
 ↓
Build
 ↓
Test
 ↓
Security Scan
 ↓
Docker Build
 ↓
Container Scan
 ↓
Push Image
 ↓
Deploy to Kubernetes
 ↓
Verify

🧰 Example GitHub Actions Workflow

name: CI-CD

on:
  push:
    branches:
      - main

permissions:
  contents: read

jobs:
  build-test-scan:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Build Docker Image
        run: |
          docker build -t myapp:${{ github.sha }} ./backend

      - name: Run Tests
        run: |
          echo "Run application tests here"

      - name: Scan Image
        run: |
          echo "Run Trivy or another approved scanner here"

The exact registry authentication and deployment steps should be configured using secure credentials and environment-specific controls.

⚙️ Jenkins Alternative

A Jenkins pipeline can follow:

Checkout
   ↓
Build
   ↓
Test
   ↓
SonarQube
   ↓
Trivy
   ↓
Docker Build
   ↓
Docker Push
   ↓
Kubernetes Deploy
   ↓
Verification

Example:

pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t myapp:${BUILD_NUMBER} ./backend'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Run tests here"'
            }
        }

        stage('Security Scan') {
            steps {
                sh 'trivy image myapp:${BUILD_NUMBER}'
            }
        }

        stage('Deploy') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }
    }
}
📊 6. Monitoring

Prometheus can collect metrics from:

Kubernetes

Nodes

Containers

Applications

Services

A typical monitoring architecture:

Kubernetes / Application
          │
          ▼
      Prometheus
          │
          ▼
       Grafana
          │
          ▼
      Dashboards

📈 Important Metrics

Monitor metrics such as:

CPU Usage
Memory Usage
Pod Status
Request Rate
Response Time
Error Rate
Network Traffic
Database Performance
Application Availability
Infrastructure Cost

🚨 7. Alerting

Alertmanager can route alerts generated by Prometheus.

Prometheus
    │
    ▼
Alertmanager
    │
    ├── Email
    ├── Slack
    ├── Teams
    └── Incident Management Tool

Example alert conditions:

CPU > 80%
Memory > 85%
Pod CrashLoopBackOff
High HTTP 5xx Rate
Application Down
High Response Latency

Alerts should be actionable and designed to avoid excessive alert noise.
🔐 8. DevSecOps Integration

Security is integrated throughout the pipeline.

Developer
    ↓
Code Scan
    ↓
Dependency Scan
    ↓
Docker Image Scan
    ↓
IaC Scan
    ↓
Kubernetes Security
    ↓
Deploy
    ↓
Runtime Monitoring

🛡️ Security Tools

SonarQube

Used for code quality and static analysis.

Source Code
    ↓
SonarQube
    ↓
Quality / Security Findings

Trivy

Can scan:

Container images

Filesystems

Dependencies

Infrastructure configuration

Example:

trivy image myapp:latest

Checkov

Used for Infrastructure as Code security scanning.

Example:

checkov -d terraform/

☸️ Kubernetes Security

Important practices:

✅ Use RBAC
✅ Follow least privilege
✅ Avoid privileged containers
✅ Avoid unnecessary root access
✅ Use NetworkPolicies where appropriate
✅ Scan images
✅ Keep cluster components updated
✅ Secure Secrets
✅ Restrict public exposure
       ▼
               AWS Load Balancer
                      │
                      ▼
              ┌───────────────┐
              │   FRONTEND    │
              │ React / Nginx │
              └───────┬───────┘
                      │
                      ▼
              ┌───────────────┐
              │    BACKEND    │
              │ Node / Python │
              └───────┬───────┘
                      │
                      ▼
              ┌───────────────┐
              │   DATABASE    │
              │ MySQL / RDS   │



🔄 10. End-to-End Deployment

The complete process:

1. Developer writes application code
            ↓
2. Push code to GitHub
            ↓
3. CI/CD pipeline starts
            ↓
4. Build application
            ↓
5. Run tests
            ↓
6. Perform security scans
            ↓
7. Build Docker image
            ↓
8. Scan Docker image
            ↓
9. Push image to registry
            ↓
10. Deploy to Kubernetes
            ↓
11. Expose through Load Balancer
            ↓
12. Monitor with Prometheus
            ↓
13. Visualize with Grafana
            ↓
14. Configure alerts
            ↓
15. Troubleshoot and optimize

🧪 11. Verification Commands

Check Kubernetes cluster:

kubectl cluster-info

Check nodes:

kubectl get nodes

Check namespaces:

kubectl get namespaces

Check deployments:

kubectl get deployments

Check pods:

kubectl get pods -A

Check services:

kubectl get svc -A

Check ingress:

kubectl get ingress -A

Check pod logs:

kubectl logs <pod-name>

Describe a pod:

kubectl describe pod <pod-name>

🐛 12. Troubleshooting Workflow

When something fails:

Check Pod
   ↓
Check Events
   ↓
Check Logs
   ↓
Check Service
   ↓
Check Endpoints
   ↓
Check Ingress / Load Balancer
   ↓
Check Application
   ↓
Check Database
   ↓
Check Monitoring

Useful commands:

kubectl get pods
kubectl describe pod <pod>
kubectl logs <pod>
kubectl get svc
kubectl get endpoints
kubectl get events --sort-by=.lastTimestamp

📦 13. Project Deliverables

The project should ideally contain:

✅ Application source code
✅ Dockerfiles
✅ Kubernetes manifests
✅ Terraform configuration
✅ CI/CD pipeline
✅ Security scanning configuration
✅ Monitoring configuration
✅ Alerting configuration
✅ Architecture diagram
✅ README documentation
✅ Deployment instructions
✅ Troubleshooting guide
📊 14. Key Metrics to Track

Category

Metrics

Application

Request Rate, Response Time, Error Rate

Kubernetes

Pod Status, Restarts, CPU, Memory

Infrastructure

CPU, Memory, Network, Disk

Database

Connections, Latency, CPU, Storage

CI/CD

Build Success Rate, Deployment Time

Security

Vulnerabilities, Failed Scans

Reliability

Uptime, MTTR, Incident Frequency

Cloud

Infrastructure Cost

💰 15. Cost Optimization

Cloud resources can become expensive if they are left running unnecesscessarily.

Best practices:

✅ Delete unused resources
✅ Use appropriate instance sizes
✅ Use autoscaling
✅ Avoid unnecessary NAT Gateway usage
✅ Monitor storage
✅ Clean unused images
✅ Review EKS node capacity
✅ Use managed services where appropriate
✅ Monitor AWS costs

For a learning project, remember to destroy temporary infrastructure when it is no longer required.

.

🛡️ 16. Production Readiness Checklist

Application
☑ Health checks
☑ Error handling
☑ Proper logging

Docker
☑ Small images
☑ Non-root user
☑ Vulnerability scanning

Kubernetes
☑ Resource requests/limits
☑ Readiness probes
☑ Liveness probes
☑ HPA where appropriate
☑ RBAC
☑ Network policies where required

CI/CD
☑ Automated tests
☑ Security scanning
☑ Approval controls
☑ Rollback strategy

Terraform
☑ Remote state
☑ Modules
☑ Version constraints
☑ Plan review

Monitoring
☑ Prometheus
☑ Grafana
☑ Alertmanager
☑ Actionable alerts

Security
☑ Secrets management
☑ Least privilege
☑ Image scanning
☑ IaC scanning
☑ Code scanning

Documentation
☑ Architecture
☑ Setup instructions
☑ Deployment instructions
☑ Troubleshooting

🌟 17. Key Learnings

This project helped connect the individual tools learned during the DevOps journey.

Linux
  ↓
Git & GitHub
  ↓
AWS
  ↓
Docker
  ↓
Kubernetes
  ↓
CI/CD
  ↓
Terraform
  ↓
Monitoring
  ↓
DevSecOps
  ↓
Real-World Project

Major lessons

DevOps is about processes and collaboration, not only tools.

Automation reduces repetitive work.

Infrastructure can be managed as code.

Containers make applications portable.

Kubernetes provides orchestration and scaling.

CI/CD enables repeatable software delivery.

Monitoring provides visibility into system health.

Security should be integrated early.

Troubleshooting is a core DevOps skill.

Documentation is essential for maintainability.

18. Interview Questions

Q1. Why use Kubernetes for this project?

Kubernetes provides container orchestration, service discovery, scaling, self-healing, and controlled application deployments.

Q2. Why use Terraform?

Terraform allows cloud infrastructure to be defined, versioned, reviewed, and provisioned as code.

Q3. Why use Docker?

Docker packages applications and their dependencies into portable containers.

Q4. How does CI/CD help?

CI/CD automates building, testing, security validation, and deployment, reducing manual effort and inconsistent deployments.

Q5. How do you monitor the application?

Prometheus collects metrics, Grafana visualizes them, and Alertmanager can route actionable alerts.

Q6. How do you secure the pipeline?

Use code scanning, dependency scanning, container scanning, IaC scanning, secret management, least privilege, protected branches, and controlled deployment.

Q7. How would you troubleshoot a failing pod?

Start with:

kubectl get pods
kubectl describe pod <pod>
kubectl logs <pod>
kubectl get events

Then check services, networking, configuration, resources, and dependencies.

Q8. How do you make the application highly available?

Use multiple replicas, appropriate Kubernetes scheduling, health probes, autoscaling, load balancing, and highly available underlying infrastructure.
🏆 19. Final Project Architecture

                           USERS
                             │
                             ▼
                    ┌─────────────────┐
                    │ AWS LoadBalancer│
                    └───18. Interview Questions

Q1. Why use Kubernetes for this project?

Kubernetes provides container orchestration, service discovery, scaling, self-healing, and controlled application deployments.

Q2. Why use Terraform?

Terraform allows cloud infrastructure to be defined, versioned, reviewed, and provisioned as code.

Q3. Why use Docker?

Docker packages applications and their dependencies into portable containers.

Q4. How does CI/CD help?

CI/CD automates building, testing, security validation, and deployment, reducing manual effort and inconsistent deployments.

Q5. How do you monitor the application?

Prometheus collects metrics, Grafana visualizes them, and Alertmanager can route actionable alerts.

Q6. How do you secure the pipeline?

Use code scanning, dependency scanning, container scanning, IaC scanning, secret management, least privilege, protected branches, and controlled deployment.

Q7. How would you troubleshoot a failing pod?

Start with:

kubectl get pods
kubectl describe pod <pod>
kubectl logs <pod>
kubectl get events

Then check services, networking, configuration, resources, and dependencies.

Q8. How do you make the application highly available?

Use multiple replicas, appropriate Kubernetes scheduling, health probes, autoscaling, load balancing, and highly available underlying infrastructure.

─────┬────────┘
                             │
                             ▼
                  ┌─────────────────────┐
                  │    AWS EKS          │
                  │                     │
                  │ ┌─────────────────┐ │
                  │ │ Frontend Pods   │ │
                  │ └────────┬────────┘ │
                  │          │          │
                  │ ┌────────▼────────┐ │
                  │ │ Backend Pods    │ │
                  │ └────────┬────────┘ │
                  └──────────┼──────────┘
                             │
                             ▼
                       ┌───────────┐
                       │ Database  │
                       │ RDS / DB  │
                       └───────────┘

        ┌────────────────────────────────────────┐
        │             DEVOPS PLATFORM             │
        │                                          │
        │ GitHub → Jenkins/GitHub Actions         │
        │ Terraform → Infrastructure              │
        │ Docker → Containers                     │
        │ Prometheus → Metrics                    │
        │ Grafana → Visualization                 │
        │ Alertmanager → Alerts                   │
        │ SonarQube → Code Security               │
        │ Trivy → Container Security              │
        │ Checkov → IaC Security                  │
        └────────────────────────────────────────┘

📈 20. 100 Days of DevOps Progress

Days 01–20 → Linux
Days 21–27 → Networking
Days 28–35 → Shell Scripting
Days 36–40 → Git & GitHub
Days 41–50 → AWS Cloud
Days 51–60 → Docker
Days 61–70 → Kubernetes
Days 71–80 → CI/CD & Jenkins
Days 81–90 → Terraform / Infrastructure as Code
Days 91–100 → Monitoring, Observability, DevSecOps & Real-World Projects

🔥 Day 98/100

██████████████████████████████████████████████████████████████████████████████████████████░░ 98%

Only 2 days remaining! 🚀

🏁 Final Takeaway

The main purpose of this project was not simply to deploy an application.

It was to understand the complete DevOps lifecycle:

PLAN
 ↓
CODE
 ↓
VERSION CONTROL
 ↓
BUILD
 ↓
TEST
 ↓
SECURITY SCAN
 ↓
CONTAINERIZE
 ↓
PROVISION
 ↓
DEPLOY
 ↓
MONITOR
 ↓
ALERT
 ↓
TROUBLESHOOT
 ↓
OPTIMIZE

A real DevOps engineer doesn't just deploy applications — they build systems that are automated, secure, observable, scalable, reliable, and maintainable.

🚀 Build → Automate → Deploy → Monitor → Secure → Improve

#100DaysOfDevOps #DevOps #AWS #Kubernetes #Docker #Terraform #Jenkins #GitHubActions #CICD #DevSecOps #Prometheus #Grafana #CloudComputing #InfrastructureAsCode #LearningInPublic
