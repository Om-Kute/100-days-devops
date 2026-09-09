🚀 Day 78 – Jenkins + Kubernetes
🎯 Objective
Integrate Jenkins with Kubernetes and automate the deployment of containerized applications into a Kubernetes cluster using Jenkins Pipelines, Kubernetes manifests, and kubectl.
🔗 Jenkins + Kubernetes
Jenkins can automate the deployment of Dockerized applications to Kubernetes.
The complete workflow:
Developer
    ↓
GitHub
    ↓
Jenkins
    ↓
Build & Test
    ↓
Docker Image
    ↓
Container Registry
    ↓
Kubernetes
    ↓
Pods
    ↓
Service
    ↓
Application 🚀
🏗️ Complete Architecture
Developer
                           │
                         git push
                           │
                           ▼
                    GitHub Repository
                           │
                        Webhook
                           │
                           ▼
                   Jenkins Controller
                           │
                           ▼
                     Jenkins Agent
                           │
                  ┌────────┴────────┐
                  ▼                 ▼
              Build/Test       Docker Build
                                    │
                                    ▼
                              Docker Image
                                    │
                                    ▼
                             Container Registry
                                    │
                                    ▼
                              Kubernetes Cluster
                                    │
                          ┌─────────┴─────────┐
                          ▼                   ▼
                       Deployment          Service
                          │                   │
                          ▼                   ▼
                         Pods              Network
                          │
                          ▼
                    Running Application
☸️ Why Jenkins + Kubernetes?
Jenkins handles automation, while Kubernetes handles container orchestration.
Jenkins
   ↓
Automate CI/CD

Docker
   ↓
Package Application

Kubernetes
   ↓
Run & Orchestrate Containers
Together they provide an automated application delivery workflow.
📋 Prerequisites
Before integrating Jenkins with Kubernetes, you should have:
✅ Jenkins Server
✅ Jenkins Agent
✅ Kubernetes Cluster
✅ kubectl
✅ kubeconfig / Kubernetes credentials
✅ Docker Image
✅ Container Registry
✅ Kubernetes YAML manifests
Verify kubectl:
kubectl version --client
Check cluster access:
kubectl get nodes
🔐 Kubernetes Credentials in Jenkins
Jenkins needs credentials to communicate securely with the Kubernetes cluster.
Conceptually:
Jenkins
   │
   ▼
Kubernetes Credentials
   │
   ▼
Kubernetes API Server
   │
   ▼
Cluster
Credentials can be configured through:
Jenkins Dashboard
       ↓
Manage Jenkins
       ↓
Credentials
       ↓
Add Credentials
The exact credential type depends on your Jenkins/Kubernetes setup.
⚠️ Security
Never hardcode:
❌ Kubernetes tokens
❌ kubeconfig secrets
❌ Cloud credentials
❌ Passwords
inside:
Jenkinsfile
Dockerfile
Git Repository
Shell Scripts
Use Jenkins Credentials and least-privilege access.
📄 Kubernetes Deployment
Example deployment.yaml:
apiVersion: apps/v1
kind: Deployment

metadata:
  name: my-app

spec:
  replicas: 3

  selector:
    matchLabels:
      app: my-app

  template:
    metadata:
      labels:
        app: my-app

    spec:
      containers:
        - name: my-app
          image: USERNAME/my-app:1.0
          ports:
            - containerPort: 8080
