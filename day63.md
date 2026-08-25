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
