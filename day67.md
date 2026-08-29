☸️ Day 67 – Kubernetes Storage
🎯 Objective

Learn how Kubernetes manages temporary and persistent storage for Pods and understand Volumes, PersistentVolumes, PersistentVolumeClaims, StorageClasses, and dynamic provisioning.
💾 Why Storage in Kubernetes?

Containers and Pods are generally ephemeral.

If a container is deleted, data stored only inside its writable container filesystem can be lost.

Pod
 │
 ▼
Container
 │
 ▼
Temporary Data
 │
 X
Pod Deleted
 │
 ▼
Data May Be Lost

For applications such as databases, file servers, and stateful applications, persistent storage is required.

Application
     │
     ▼
    Pod
     │
     ▼
Persistent Storage
     │
     ▼
Data Survives Pod Lifecycle
