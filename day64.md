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
📊 Check Deployment
kubectl get deployment nginx-deployment

Detailed information:

kubectl describe deployment nginx-deployment

Example:

NAME               READY   UP-TO-DATE   AVAILABLE
nginx-deployment   3/3     3            3
🔢 Scaling a Deployment

Scale up:

kubectl scale deployment nginx-deployment --replicas=5

Check:

kubectl get pods

Architecture:

Deployment
     │
     ▼
ReplicaSet
     │
 ┌───┼───┬───┬───┐
 ▼   ▼   ▼   ▼   ▼
Pod Pod Pod Pod Pod
📉 Scale Down
kubectl scale deployment nginx-deployment --replicas=2

Check:

kubectl get pods

Kubernetes works toward the desired state:

Desired = 2
Actual  = 2
🔄 Rolling Updates

A rolling update gradually replaces old Pods with new Pods.

Example:

Version 1
   │
   ▼
ReplicaSet v1
   │
   ├── Pod v1
   ├── Pod v1
   └── Pod v1

Update:

Version 2
   │
   ▼
ReplicaSet v2
   │
   ├── Pod v2
   ├── Pod v2
   └── Pod v2

Conceptually:

Old ReplicaSet
      │
      ▼
New ReplicaSet
      │
      ▼
New Pods gradually replace old Pods
🔧 Update Image

Change the Deployment image:

kubectl set image deployment/nginx-deployment nginx=nginx:1.26

Check rollout:

kubectl rollout status deployment/nginx-deployment
📈 Rolling Update Flow
Old Pods
   │
   ▼
Create New ReplicaSet
   │
   ▼
Create New Pods
   │
   ▼
Terminate Old Pods Gradually
   │
   ▼
New Version Running
Running
🔍 Rollout Status
kubectl rollout status deployment/nginx-deployment

This allows you to monitor whether the rollout has completed successfully.

📜 Rollout History

View deployment history:

kubectl rollout history deployment/nginx-deployment

View a specific revision:

kubectl rollout history deployment/nginx-deployment --revision=2
↩️ Rollback

If a new deployment version causes problems, rollback to the previous revision:

kubectl rollout undo deployment/nginx-deployment

Check:

kubectl rollout status deployment/nginx-deployment

Architecture:

Version 1
   │
   ▼
Version 2
   │
   X
Problem
   │
   ▼
Rollback
   │
   ▼
Version 1
