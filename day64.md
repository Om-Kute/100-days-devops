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
📄 Deployment YAML

Example:

apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-deployment

spec:
  replicas: 3

  selector:
    matchLabels:
      app: nginx

  template:
    metadata:
      labels:
        app: nginx

 spec:
      containers:
        - name: nginx
          image: nginx:1.25
          ports:
            - containerPort: 80
🔍 Deployment YAML Explanation
apiVersion
apiVersion: apps/v1

Specifies the Kubernetes API version.

kind
kind: Deployment

Defines the resource type.

replicas
replicas: 3

Requests three Pod replicas.

selector
selector:
  matchLabels:
    app: nginx

Defines which Pods are managed by the Deployment.

template

Defines the Pod template used to create new Pods.

🚀 Create Deployment

Create a file:

nano deployment.yaml

Apply it:

kubectl apply -f deployment.yaml

Check Deployment:

kubectl get deployments

Check ReplicaSets:

kubectl get replicasets

Check Pods:

kubectl get pods
