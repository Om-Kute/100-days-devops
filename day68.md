☸️ Day 68 – Kubernetes Ingress & Networking
🎯 Objective

Learn how Kubernetes provides Pod-to-Pod communication, Service networking, external access, HTTP/HTTPS routing, Ingress, TLS, and basic NetworkPolicies.
🌐 Kubernetes Networking

Kubernetes provides a networking model where Pods can communicate across the cluster.

Pod A
  │
  │
  ▼
Pod B

Each Pod receives its own IP address within the cluster networking model.

However, Pod IPs are ephemeral and should generally not be used directly by clients.

For stable access, Kubernetes Services are used.
🏗️ Kubernetes Networking Overview
                    Internet
                       │
                       ▼
                    Ingress
                       │
                       ▼
                    Service
                       │
             ┌─────────┼─────────┐
             ▼         ▼         ▼
           Pod 1     Pod 2     Pod 3

For HTTP/HTTPS applications, a common architecture is:

Client
  │
  ▼
Ingress
  │
  ▼
Service
  │
  ▼
Pods
📦 Kubernetes Service

A Service provides a stable network endpoint for a set of Pods.

             Service
                │
        ┌───────┼───────┐
        ▼       ▼       ▼
      Pod 1   Pod 2   Pod 3

If a Pod is replaced and its IP changes, the Service continues providing a stable endpoint.
🔵 ClusterIP

ClusterIP is the default Service type.

It exposes the Service internally within the cluster.

apiVersion: v1
kind: Service

metadata:
  name: app-service

spec:
  type: ClusterIP

  selector:
    app: web

  ports:
    - port: 80
      targetPort: 8080

Architecture:

Inside Cluster
      │
      ▼
ClusterIP Service
      │
      ▼
    Pods
Use Case

Internal communication between application components.
🟠 NodePort

A NodePort exposes a Service on a port on each node.

Example:

apiVersion: v1
kind: Service

metadata:
  name: web-service

spec:
  type: NodePort

  selector:
    app: web

  ports:
    - port: 80
      targetPort: 8080
      nodePort: 30080

Architecture:

External Client
      │
      ▼
Node IP:30080
      │
      ▼
   Service
      │
      ▼
     Pods
