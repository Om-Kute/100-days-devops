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

Service
   │
   │ selector: app=nginx
   │
   ├── Pod app=nginx ✅
   ├── Pod app=nginx ✅
   └── Pod app=backend ❌
