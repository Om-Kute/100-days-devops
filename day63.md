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
2️⃣ Multi-Container Pod

A Pod can contain multiple containers when those containers are tightly coupled and need to share resources.

             POD
       ┌──────┴──────┐
       ▼             ▼
 Application      Sidecar
 Container        Container

Example:

apiVersion: v1
kind: Pod

metadata:
  name: multi-container-pod

spec:
  containers:

    - name: app
      image: nginx:latest
      ports:
        - containerPort: 80

    - name: sidecar
      image: busybox
      command:
        - sh
        - -c
        - |
          while true; do
            echo "Sidecar running"
            sleep 10
          done

Both containers share the same Pod network namespace.

🔄 3️⃣ Init Containers

Init Containers run before the main application containers.

Pod
 │
 ▼
Init Container
 │
 ▼
Application Container

Example:

apiVersion: v1
kind: Pod

metadata:
  name: init-demo

spec:

  initContainers:

    - name: init
      image: busybox
      command:
        - sh
        - -c
        - echo "Initializing application"

  containers:

    - name: app
      image: nginx:latest
Use Cases

Init Containers can be used for:

Initialization tasks
Waiting for dependencies
Preparing files
Configuration setup
Database preparation
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
