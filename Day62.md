☸️ Day 62 – Kubernetes Architecture & Components
🎯 Objective
Understand the internal architecture of Kubernetes and learn how the Control Plane, Worker Nodes, and Kubernetes components work together to deploy and manage containerized applications.
🏗️ Kubernetes Architecture
A Kubernetes cluster consists mainly of:
                    Kubernetes Cluster
                           │
              ┌────────────┴────────────┐
              │                         │
        Control Plane              Worker Nodes
              │                         │
      ┌───────┼────────┐          ┌─────┴─────┐
      │       │        │          │           │
   API     Scheduler Controller Kubelet   Kube-Proxy
  Server             Manager       │
      │       │        │           ▼
      └───────┼────────┘          Pods
              │
             etcd
Simple Concept
Control Plane → Makes decisions
Worker Node   → Runs applications
🎛️ Control Plane
The Control Plane manages the overall state of the Kubernetes cluster.
Main components:
Control Plane
     │
     ├── API Server
     ├── Scheduler
     ├── Controller Manager
     └── etcd
The Control Plane decides what should happen, while Worker Nodes execute the workloads.
