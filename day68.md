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
