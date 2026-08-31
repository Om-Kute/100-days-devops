☸️ Day 69 – Kubernetes Security & RBAC
🎯 Objective
Learn how to secure Kubernetes clusters and control access to Kubernetes resources using Role-Based Access Control (RBAC), ServiceAccounts, Admission Controllers, and Pod Security Standards.
🔐 Kubernetes Security
Kubernetes security protects:
Cluster resources
Applications
APIs
Secrets
Workloads
Network communication
User and application access
A simplified security model:
User / Application
        │
        ▼
 Authentication
        │
        ▼
 Authorization
        │
        ▼
 Admission Control
        │
        ▼
 Kubernetes API
        │
        ▼
 Cluster Resources
