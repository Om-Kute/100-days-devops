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
📁 2. hostPath

hostPath mounts a file or directory from the Kubernetes node into a Pod.

Example:

volumes:
  - name: host-data
    hostPath:
      path: /mnt/data
      type: DirectoryOrCreate

Architecture:

Worker Node
     │
     ▼
 /mnt/data
     │
     ▼
   Pod
⚠️ Important

hostPath ties the workload to a particular node's filesystem and is generally not the preferred storage mechanism for portable production applications.
🗄️ PersistentVolume (PV)

A PersistentVolume is a storage resource available in the Kubernetes cluster.

It can be:

Provisioned manually
Provisioned dynamically through a StorageClass

Example:

apiVersion: v1
kind: PersistentVolume

metadata:
  name: manual-pv

spec:
  capacity:
    storage: 5Gi

  accessModes:
    - ReadWriteOnce

  persistentVolumeReclaimPolicy: Retain

  hostPath:
    path: /mnt/data
📋 PV Components

A PersistentVolume can define:

PV
 │
 ├── Capacity
 ├── Access Modes
 ├── Reclaim Policy
 ├── Storage Class
 └── Storage Source
🔗 PersistentVolumeClaim (PVC)

A PersistentVolumeClaim is a request for storage made by a user or workload.

Example:

apiVersion: v1
kind: PersistentVolumeClaim

metadata:
  name: my-pvc

spec:
  accessModes:
    - ReadWriteOnce

  resources:
    requests:
      storage: 5Gi

Concept:

Application
     │
     ▼
    PVC
     │
     ▼
    PV
     │
     ▼
Storage
⚖️ PV vs PVC
PersistentVolume	PersistentVolumeClaim
Storage resource	Storage request
Represents available storage	Requests storage
Usually managed by cluster/admin or provisioner	Usually created by application/user
Provides capacity	Specifies required capacity
Can be dynamically provisioned	Can trigger dynamic provisioning
Easy Memory Trick
PV  → Provides Storage
PVC → Requests Storage
🏷️ StorageClass

A StorageClass defines how storage should be dynamically provisioned.

Example:

apiVersion: storage.k8s.io/v1
kind: StorageClass

metadata:
  name: fast-storage

provisioner: example.com/provisioner

reclaimPolicy: Delete

volumeBindingMode: WaitForFirstConsumer

The exact provisioner depends on the Kubernetes environment.

For example, cloud environments provide their own CSI-based storage drivers.
⚡ Dynamic Provisioning

With dynamic provisioning, Kubernetes can automatically create storage when a PVC requests it.

User creates PVC
       │
       ▼
StorageClass
       │
       ▼
Provisioner
       │
       ▼
PersistentVolume
       │
       ▼
PVC Bound
       │
       ▼
Pod Uses Storage

This avoids manually creating every PV.

🔄 Storage Flow

The complete relationship can be remembered as:

Pod
 │
 ▼
PVC
 │
 ▼
PV
 │
 ▼
Actual Storage
Example
MySQL Pod
    │
    ▼
mysql-pvc
    │
    ▼
mysql-pv
    │
    ▼
EBS / Disk / Cloud Storage
🔐 Access Modes

Kubernetes storage can support different access modes depending on the storage implementation.

ReadWriteOnce (RWO)

Volume can be mounted read-write by a single node.

Node 1
  │
  ▼
Volume
ReadOnlyMany (ROX)

Volume can be mounted read-only by multiple nodes.

Node 1 ──┐
Node 2 ──┼──► Volume
Node 3 ──┘
ReadWriteMany (RWX)

Volume can be mounted read-write by multiple nodes, if supported by the storage backend.

Node 1 ──┐
Node 2 ──┼──► Volume
Node 3 ──┘

Supported access modes depend on the storage provider and CSI driver.

🔄 PV Lifecycle

A PersistentVolume can move through states such as:

Available
    │
    ▼
Bound
    │
    ▼
Released
    │
    ▼
Reclaimed / Deleted

Common PV phases:

Available
Bound
Released
Failed
🗑️ Reclaim Policies

Common reclaim policies include:

Retain

The storage resource is retained after the PVC is deleted.

PVC Deleted
     │
     ▼
PV Retained
     │
     ▼
Data Can Be Recovered/Managed
Delete

The dynamically provisioned storage is deleted according to the storage provisioner's behavior.

PVC Deleted
     │
     ▼
Provisioned Storage Deleted

Choose the policy according to the application's data-retention requirements.

📦 Pod Using PVC

Example:

apiVersion: v1
kind: Pod

metadata:
  name: nginx-pvc-pod

spec:

  containers:

    - name: nginx
      image: nginx:alpine

      volumeMounts:
        - name: website-data
          mountPath: /usr/share/nginx/html

  volumes:

    - name: website-data

      persistentVolumeClaim:
        claimName: my-pvc

Architecture:

        Nginx Pod
            │
            ▼
          PVC
            │
            ▼
           PV
            │
            ▼
      Actual Storage
