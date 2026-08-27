# ☸️ Day 65 – Kubernetes Services

## 🎯 Objective

Learn how Kubernetes Services provide **stable networking, service discovery, and traffic distribution** for applications running inside Pods.
# 🌐 What is a Kubernetes Service?

A Kubernetes **Service** is an abstraction that provides a stable network endpoint for accessing a group of Pods.

Pods are ephemeral. Their IP addresses can change when Pods are recreated.

A Service provides a stable way to reach those Pods.

             Client
                │
                ▼
        Kubernetes Service
        Stable IP / DNS Name
                │
        ┌───────┼───────┐
        ▼       ▼       ▼
      Pod 1   Pod 2   Pod 3
❓ Why Do We Need Services?

Consider a Deployment with three Pods:

Deployment
    │
    ▼
┌────┼────┐
▼    ▼    ▼
Pod 1 Pod 2 Pod 3

Pod IPs may change:

Pod 1 → 10.244.1.10
Pod 2 → 10.244.1.11
Pod 3 → 10.244.1.12

If a Pod is deleted:

Pod 2 ❌

Kubernetes may create a replacement:

Pod 4 → 10.244.1.20

The IP changed.

A Service solves this problem:

Client
  │
  ▼
Service
Stable DNS/IP
  │
  ├── Pod 1
  ├── Pod 3
  └── Pod 4
Key Concept
Pod IP       → Can change
Service IP   → Stable
Service DNS  → Stable
Service Architecture
                    Client
                       │
                       ▼
              Kubernetes Service
                       │
                 Label Selector
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
        Pod 1         Pod 2        Pod 3

The Service uses selectors to identify the Pods that should receive traffic.

🏷️ Service Selectors

Example Pods:

labels:
  app: nginx

Service selector:

selector:
  app: nginx

The Service sends traffic to Pods matching:

app=nginx

Concept:
❌
🔵 1. ClusterIP

ClusterIP is the default Service type.

It provides an internal IP address that can normally be accessed from within the cluster.

             Cluster
                │
        ┌───────┴───────┐
        │               │
      Client          Service
                        │
                 ClusterIP
                        │
              ┌─────────┼─────────┐
              ▼         ▼         ▼
             Pod       Pod       Pod

Example:

apiVersion: v1
kind: Service

metadata:
  name: nginx-service

spec:
  type: ClusterIP

  selector:
    app: nginx

  ports:
    - port: 80
      targetPort: 80

Create:

kubectl apply -f service.yaml
Service
   │
   │ selector: app=nginx
   │
   ├── Pod app=nginx ✅
   ├── Pod app=nginx ✅
   └── Pod app=backend ❌
🟢 2. NodePort

NodePort exposes a Service on a port on each node.

Conceptually:

External Client
      │
      ▼
Node IP:NodePort
      │
      ▼
Service
      │
      ▼
Pods

Example:

apiVersion: v1
kind: Service

metadata:
  name: nginx-nodeport

spec:
  type: NodePort

  selector:
    app: nginx

  ports:
    - port: 80
      targetPort: 80
      nodePort: 30080

Access:

http://NODE_IP:30080

The exact accessible address depends on your cluster networking and environment.

Use Cases
Development
Testing
Lab environments
Some self-managed/on-premises setups
🟠 3. LoadBalancer

LoadBalancer is commonly used in cloud environments where the platform can provision an external load balancer.

              Internet
                  │
                  ▼
        Cloud Load Balancer
                  │
        ┌─────────┼─────────┐
        ▼         ▼         ▼
      Node 1    Node 2    Node 3
        │         │         │
        └─────────┼─────────┘
                  ▼
               Service
                  │
             ┌────┼────┐
             ▼    ▼    ▼
            Pod  Pod  Pod

Example:

apiVersion: v1
kind: Service

metadata:
  name: nginx-lb

spec:
  type: LoadBalancer

  selector:
    app: nginx

  ports:
    - port: 80
      targetPort: 80
Use Case

Useful when exposing applications externally through a cloud provider's load-balancing integration.
🟣 4. ExternalName

ExternalName maps a Kubernetes Service name to an external DNS name.

Example:

apiVersion: v1
kind: Service

metadata:
  name: external-db

spec:
  type: ExternalName
  externalName: database.example.com

Concept:

Application
     │
     ▼
external-db
     │
     ▼
database.example.com

Unlike ClusterIP, NodePort, or LoadBalancer, ExternalName does not create a normal proxying Service.

📊 Service Types Comparison
Type	Main Purpose	Typical Access
ClusterIP	Internal application access	Inside cluster
NodePort	Expose through node port	Outside cluster
LoadBalancer	External cloud load balancing	Internet/external clients
ExternalName	DNS alias to external service	External dependency
Easy Memory Trick
ClusterIP    → Internal
NodePort     → Node IP + Port
LoadBalancer → External Load Balancer
ExternalName → External DNS
📄 Service YAML

Example:

apiVersion: v1
kind: Service

metadata:
  name: nginx-service

spec:
  type: ClusterIP

  selector:
    app: nginx

  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
🔍 Service YAML Explanation
apiVersion
    ↓
Kubernetes API version

kind
    ↓
Service

metadata
    ↓
Service name and labels

spec
    ↓
Desired Service configuration

type
    ↓
ClusterIP / NodePort / LoadBalancer / ExternalName

selector
    ↓
Selects backend Pods

port
    ↓
Service port

targetPort
    ↓
Pod/container destination port
🔌 port vs targetPort

This is an important concept.

ports:
  - port: 80
    targetPort: 8080

Architecture:

Client
  │
  ▼
Service :80
  │
  ▼
Pod :8080
Remember
port       → Service port
targetPort → Pod application port
🔍 Check Services

List Services:

kubectl get services

Short form:

kubectl get svc

More information:

kubectl get svc -o wide
📋 Describe Service
kubectl describe svc nginx-service

This can show:

Service type
Cluster IP
Ports
Selector
Endpoints
Events
