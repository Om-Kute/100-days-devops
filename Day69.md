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
🔑 Authentication vs Authorization
Authentication
Authentication answers:
Who are you?
Examples:
User identity
ServiceAccount
Certificates
OIDC identity provider
Identity
   │
   ▼
Authentication
   │
   ▼
Verified Identity
Authorization
Authorization answers:
What are you allowed to do?
RBAC is one of Kubernetes' primary authorization mechanisms.
Authenticated User
       │
       ▼
 Authorization
       │
       ▼
Allowed / Denied
🛡️ What is RBAC?
RBAC = Role-Based Access Control
RBAC controls which users, groups, and ServiceAccounts can perform which actions on Kubernetes resources.
Subject
   │
   ▼
Role / ClusterRole
   │
   ▼
RoleBinding / ClusterRoleBinding
   │
   ▼
Kubernetes Resources
