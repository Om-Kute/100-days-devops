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
