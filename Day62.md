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
🌐 1. Kubernetes API Server
The API Server is the central communication point of Kubernetes.
Almost all cluster operations go through the Kubernetes API.
kubectl
   │
   ▼
API Server
   │
   ▼
Kubernetes Cluster
Example:
kubectl get nodes
The command communicates with the API Server.
Responsibilities
Accept API requests
Authenticate and authorize requests
Validate Kubernetes objects
Update cluster state
Communicate with other control-plane components
📅 2. Kubernetes Scheduler
The Scheduler decides which Worker Node should run a newly scheduled Pod.
New Pod
   │
   ▼
Scheduler
   │
   ├── Check resources
   ├── Check constraints
   ├── Check policies
   └── Select suitable node
   │
   ▼
Worker Node
The Scheduler considers factors such as:
CPU
Memory
Node availability
Resource requests
Node selectors
Affinity/anti-affinity
Taints and tolerations
🔄 3. Controller Manager
The Controller Manager runs controllers that continuously compare:
Desired State
      ↓
Actual State
If they differ, controllers work to reconcile the cluster.
Example:
Desired:
3 Pods

Actual:
2 Pods

Controller
    ↓
Create replacement Pod
    ↓
3 Pods
Examples of controllers include:
Node controller
Deployment controller
ReplicaSet controller
Job controller
EndpointSlice-related controllers
