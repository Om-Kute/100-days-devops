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
🧩 RBAC Building Blocks
RBAC
 │
 ├── Role
 ├── ClusterRole
 ├── RoleBinding
 └── ClusterRoleBinding
📋 Role
A Role defines permissions within a specific namespace.
Example:
apiVersion: rbac.authorization.k8s.io/v1
kind: Role

metadata:
  name: pod-reader
  namespace: dev

rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["get", "list", "watch"]
This Role allows reading Pods in the dev namespace.
🌐 ClusterRole
A ClusterRole defines permissions that can apply cluster-wide or be bound into a namespace.
Example:
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole

metadata:
  name: cluster-view

rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["get", "list", "watch"]
A ClusterRole can be used with a ClusterRoleBinding for cluster-wide access, or with a RoleBinding to grant its permissions within a specific namespace.
🔗 RoleBinding
A RoleBinding grants a Role's permissions to a subject within a namespace.
Example:
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding

metadata:
  name: pod-reader-binding
  namespace: dev

subjects:
  - kind: User
    name: om

roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
Architecture:
User
 │
 ▼
RoleBinding
 │
 ▼
Role
 │
 ▼
Pods in dev namespace
🔗 ClusterRoleBinding
A ClusterRoleBinding grants a ClusterRole's permissions across the cluster.
Example:
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding

metadata:
  name: cluster-view-binding

subjects:
  - kind: Group
    name: devops-team

roleRef:
  kind: ClusterRole
  name: cluster-view
  apiGroup: rbac.authorization.k8s.io
Architecture:
Group
 │
 ▼
ClusterRoleBinding
 │
 ▼
ClusterRole
 │
 ▼
Cluster Resources
