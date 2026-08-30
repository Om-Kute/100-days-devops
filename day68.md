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
