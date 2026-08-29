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
🧩 Kubernetes Storage Components
                    Pod
                     │
                     ▼
                    PVC
          PersistentVolumeClaim
                     │
                     ▼
                    PV
            PersistentVolume
                     │
                     ▼
              Actual Storage
          Cloud / Disk / Storage
Simple Memory Trick
PVC → Request for Storage
PV  → Storage Resource
Pod → Uses PVC
📦 Kubernetes Volumes

A Kubernetes Volume provides storage that can be mounted into containers within a Pod.

Some common volume types include:

emptyDir
hostPath
configMap
secret
persistentVolumeClaim
🟢 1. emptyDir

emptyDir creates temporary storage for a Pod.

Example:

apiVersion: v1
kind: Pod

metadata:
  name: emptydir-demo

spec:
  containers:

    - name: app
      image: nginx:alpine

      volumeMounts:
        - name: shared-data
          mountPath: /data

  volumes:

    - name: shared-data
      emptyDir: {}

Architecture:

Pod
 │
 ├── Container
 │
 └── emptyDir Volume

The volume exists while the Pod exists.

Use Cases
Temporary files
Cache
Sharing files between containers in the same Pod
Scratch space
