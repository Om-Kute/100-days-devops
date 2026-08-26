# ☸️ Day 64 – Kubernetes Deployments & ReplicaSets

## 🎯 Objective

Learn how Kubernetes **Deployments and ReplicaSets** manage application Pods, maintain the desired number of replicas, perform rolling updates, scale applications, and provide rollback capabilities.
# 🔄 ReplicaSet vs Deployment

A ReplicaSet ensures that a specified number of Pod replicas are running.

A Deployment manages ReplicaSets and provides higher-level application deployment features.
text
Deployment
     │
     ▼
ReplicaSet
     │
     ▼
  Pods
  🔢 What is a ReplicaSet?

A ReplicaSet maintains a stable number of identical Pods.

For example:

Desired Replicas = 3

        ReplicaSet
             │
      ┌──────┼──────┐
      ▼      ▼      ▼
    Pod 1  Pod 2  Pod 3

If one Pod fails:

Pod 1
Pod 2
Pod 3
  │
  X
Pod 2 fails
  │
  ▼
ReplicaSet creates replacement
  │
  ▼
Pod 4

The desired number of replicas remains:

3 Pods
🚀 What is a Deployment?

A Deployment provides declarative management for applications running in Pods.

It manages ReplicaSets and supports:

Scaling
Rolling updates
Rollbacks
Version management
Desired-state management

Architecture:

Deployment
     │
     ├── ReplicaSet v1
     │       ├── Pod
     │       ├── Pod
     │       └── Pod
     │
     └── ReplicaSet v2
             ├── Pod
             ├── Pod
             └── Pod
🏗️ Deployment Architecture
                 Deployment
                     │
             ┌───────┴───────┐
             ▼               ▼
        ReplicaSet v1    ReplicaSet v2
             │               │
             ▼               ▼
          Old Pods         New Pods

During an update, Kubernetes gradually moves from the old ReplicaSet to the new ReplicaSet.
