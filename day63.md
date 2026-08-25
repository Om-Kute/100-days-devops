☸️ Day 63 – Kubernetes Pods & Containers
🎯 Objective

Learn about Kubernetes Pods, the smallest deployable unit in Kubernetes, and understand how containers are created, managed, networked, and stored inside Pods.
📦 What is a Pod?

A Pod is the smallest deployable unit in Kubernetes.

A Pod represents one or more containers that are deployed and managed together.

Pod
 │
 ├── Container 1
 │
 └── Container 2

Containers inside the same Pod share:

Network namespace
IP address
Port space
Volumes
🐳 Pod vs Container
Kubernetes
     │
     ▼
    Pod
     │
     ├── Container
     ├── Network
     └── Storage
Pod	Container
Kubernetes workload unit	Runtime process
Can contain one or more containers	Usually runs one application process
Managed by Kubernetes	Managed by container runtime
Shares network and storage with containers in the Pod	Has its own process environment
Has a lifecycle/state	Has a container lifecycle
Easy Memory Trick
Container → Application process
Pod       → Kubernetes execution environment
1️⃣ Single-Container Pod

Most Kubernetes workloads use one main application container per Pod.

       POD
        │
        ▼
 ┌─────────────┐
 │   Nginx     │
 │  Container  │
 └─────────────┘

Example:

apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
