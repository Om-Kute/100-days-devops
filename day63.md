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
now give me txt to post with these img
☸️ Day 63/100 – Kubernetes Pods & Containers 🚀

Continuing my #100DaysOfDevOps journey, today I learned about one of the most important building blocks of Kubernetes — Pods. A Pod is the smallest deployable unit in Kubernetes and represents one or more containers that run together. I learned the difference between single-container Pods, multi-container Pods, and init-container patterns, along with how containers inside the same Pod share the same network namespace and can communicate using `localhost`. I also explored the Pod lifecycle, including Pending, Running, Succeeded, Failed, Unknown, and Terminating states, and learned that Pods are ephemeral and are normally managed by higher-level controllers such as Deployments and ReplicaSets rather than created directly for production workloads. I practiced important commands such as `kubectl run`, `kubectl get pods`, `kubectl describe pod`, `kubectl logs`, `kubectl exec`, `kubectl apply`, and `kubectl delete pod`, and also learned how Pods can share storage through volumes. 💡 My key takeaway is that a Pod provides the execution environment for containers in Kubernetes, including shared networking and storage, while Kubernetes controllers are responsible for maintaining application availability.

☸️ Kubernetes Progress:
✅ Day 61 – Kubernetes Fundamentals
✅ Day 62 – Kubernetes Architecture & Components
✅ Day 63 – Pods & Containers

🔜 Day 64 – Deployments & ReplicaSets

#100DaysOfDevOps #Kubernetes #K8s #KubernetesPods #Containers #DevOps #Docker #ContainerOrchestration #CloudComputing #Linux #AWS #DevOpsEngineer #LearningInPublic
give Readme.md file
☸️ Day 63 – Kubernetes Pods & Containers
🎯 Objective

Learn about Kubernetes Pods, the smallest deployable unit in Kubernetes, and understand how containers are created, managed, networked, and stored inside Pods.

📚 Topics Covered
What is a Pod?
Pod vs Container
Single-container Pods
Multi-container Pods
Init Containers
Pod lifecycle
Pod networking
Shared storage
Pod YAML
kubectl run
kubectl apply
kubectl get pods
kubectl describe
kubectl logs
kubectl exec
kubectl delete
Pod best practices
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

spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
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
now give me txt to post with these img
☸️ Day 63/100 – Kubernetes Pods & Containers 🚀

Continuing my #100DaysOfDevOps journey, today I learned about one of the most important building blocks of Kubernetes — Pods. A Pod is the smallest deployable unit in Kubernetes and represents one or more containers that run together. I learned the difference between single-container Pods, multi-container Pods, and init-container patterns, along with how containers inside the same Pod share the same network namespace and can communicate using `localhost`. I also explored the Pod lifecycle, including Pending, Running, Succeeded, Failed, Unknown, and Terminating states, and learned that Pods are ephemeral and are normally managed by higher-level controllers such as Deployments and ReplicaSets rather than created directly for production workloads. I practiced important commands such as `kubectl run`, `kubectl get pods`, `kubectl describe pod`, `kubectl logs`, `kubectl exec`, `kubectl apply`, and `kubectl delete pod`, and also learned how Pods can share storage through volumes. 💡 My key takeaway is that a Pod provides the execution environment for containers in Kubernetes, including shared networking and storage, while Kubernetes controllers are responsible for maintaining application availability.

☸️ Kubernetes Progress:
✅ Day 61 – Kubernetes Fundamentals
✅ Day 62 – Kubernetes Architecture & Components
✅ Day 63 – Pods & Containers

🔜 Day 64 – Deployments & ReplicaSets

#100DaysOfDevOps #Kubernetes #K8s #KubernetesPods #Containers #DevOps #Docker #ContainerOrchestration #CloudComputing #Linux #AWS #DevOpsEngineer #LearningInPublic
give Readme.md file
☸️ Day 63 – Kubernetes Pods & Containers
🎯 Objective

Learn about Kubernetes Pods, the smallest deployable unit in Kubernetes, and understand how containers are created, managed, networked, and stored inside Pods.

📚 Topics Covered
What is a Pod?
Pod vs Container
Single-container Pods
Multi-container Pods
Init Containers
Pod lifecycle
Pod networking
Shared storage
Pod YAML
kubectl run
kubectl apply
kubectl get pods
kubectl describe
kubectl logs
kubectl exec
kubectl delete
Pod best practices
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

spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
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
📄 Pod YAML Structure

A Kubernetes Pod manifest generally contains:

apiVersion:
kind:
metadata:
spec:

Example:

apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod
  labels:
    app: nginx

spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
Explanation
apiVersion → Kubernetes API version
kind       → Resource type
metadata   → Name, labels, annotations
spec       → Desired configuration
🚀 Create Pod Using kubectl

Quickly create a Pod:

kubectl run nginx --image=nginx

Check:

kubectl get pods
📋 Get Pods
kubectl get pods

More information:

kubectl get pods -o wide

All namespaces:

kubectl get pods -A

Watch Pods:

kubectl get pods -w
🔍 Describe Pod
kubectl describe pod nginx

This provides information about:

Pod configuration
Node
Containers
Events
IP address
Volumes
Conditions
📜 View Pod Logs
kubectl logs nginx

For a specific container in a multi-container Pod:

kubectl logs nginx -c app

Follow logs:

kubectl logs -f nginx
