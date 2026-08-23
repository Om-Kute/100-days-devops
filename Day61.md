☸️ Day 61 – Kubernetes Fundamentals
🎯 Objective
Start the Kubernetes phase of the 100 Days of DevOps journey and understand the fundamentals of Kubernetes, container orchestration, clusters, nodes, Pods, Control Plane components, and kubectl.
☸️ What is Kubernetes?
Kubernetes (K8s) is an open-source platform for automating the deployment, scaling, and management of containerized applications.
Docker allows us to build and run containers, while Kubernetes helps manage containers across a cluster.
Docker
  │
  ▼
Build & Run Containers
  │
  ▼
Kubernetes
  │
  ├── Deploy
  ├── Scale
  ├── Monitor
  ├── Self-Heal
  └── Manage Containers
🐳 Docker vs Kubernetes
Docker
Kubernetes
Builds and runs containers
Orchestrates containers
Container runtime/tooling
Container orchestration platform
Usually manages containers on a host
Manages workloads across a cluster
Manual scaling
Automated scaling capabilities
Basic container networking
Service discovery and networking
Individual container management
Application/workload management
Simple Memory Trick
Docker      → Container
Kubernetes  → Container Orchestration
Why Kubernetes?
Kubernetes provides features that help operate containerized applications reliably.
Major Benefits
Automated deployment
Scaling
Self-healing
Service discovery
Load balancing
Rolling updates
Rollbacks
Resource management
Declarative configuration
High availability
Container orchestration
🏗️ Kubernetes Architecture
A Kubernetes cluster generally contains:
                 Kubernetes Cluster
                        │
          ┌─────────────┴─────────────┐
          │                           │
     Control Plane                Worker Nodes
          │                           │
   ┌──────┼──────┐             ┌──────┴──────┐
   │      │      │             │             │
 API   Scheduler Controller   Kubelet     Kubelet
Server          Manager         │             │
   │             │              ▼             ▼
   └──── etcd ───┘            Pods          Pods
🎛️ Control Plane
The Control Plane manages the overall Kubernetes cluster.
Important components include:
Control Plane
     │
     ├── API Server
     ├── Scheduler
     ├── Controller Manager
     └── etcd
