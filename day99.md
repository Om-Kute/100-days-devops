🚀 Day 99/100 – DevOps Project Optimization & Best Practices

⚙️ Making the DevOps Project Production-Ready

Day 99 focuses on optimizing the real-world DevOps project developed during the previous stages of the 100 Days of DevOps journey.

The objective is to take the existing application and infrastructure and improve its:
⚡ Performance
📈 Scalability
🔐 Security
🛡️ Reliability
💰 Cost efficiency
🔄 Automation
📊 Observability
🧹 Maintainability

The goal is not simply to make the application work, but to make it production-ready and easier to operate.
🏗️ Optimized DevOps Architecture

                         USERS
                           │
                           ▼
                     AWS Route 53
                           │
                           ▼
                    AWS Load Balancer
                           │
                           ▼
                 ┌───────────────────┐
                 │     AWS EKS       │
                 │                   │
                 │ ┌───────────────┐ │
                 │ │   Frontend    │ │
                 │ │    Pods       │ │
                 │ └───────┬───────┘ │
                 │         │         │
                 │ ┌───────▼───────┐ │
                 │ │    Backend    │ │
                 │ │     Pods      │ │
                 │ └───────┬───────┘ │
                 └─────────┼─────────┘
                           │
                           ▼
                       Database
                           │
                           ▼
                         RDS

       ┌─────────────────────────────────────┐
       │          DevOps Platform            │
       │                                     │
       │ GitHub → CI/CD → Docker → EKS      │
       │ Terraform → Infrastructure         │
       │ Prometheus → Metrics               │
       │ Grafana → Dashboards               │
       │ Alertmanager → Alerts              │
       │ SonarQube → Code Security          │
       │ Trivy → Container Security         │
       │ Checkov → IaC Security             │
       └─────────────────────────────────────┘
📊 1. Optimization Areas

The project is optimized across seven major areas:
Area
Objective
Performance
Faster response and efficient resource usage
Scalability
Handle increasing traffic
Reliability
Reduce failures and downtime
Security
Reduce vulnerabilities and attack surface
Cost
Eliminate unnecessary cloud spending
Automation
Reduce manual operations
Observability
Improve visibility into systems
⚡ 2. Performance Optimization

Performance optimization ensures that applications respond quickly while using resources efficiently.

Application-level improvements

✅ Optimize database queries
✅ Reduce unnecessary API calls
✅ Use caching
✅ Compress static assets
✅ Optimize frontend bundles
✅ Remove unnecessary dependencies
✅ Use asynchronous processing where appropriate
🐳 Docker Performance Optimization

Large container images can increase:

Build time

Push/pull time

Storage requirements

Deployment time

Use multi-stage builds

Example:

# Build stage
FROM node:22-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . .

RUN npm run build


# Production stage
FROM nginx:alpine

COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80

Benefits

Smaller Image
↓
Faster Push
      ↓
Faster Pull
      ↓
Faster Deployment
🧹 Docker Best Practices

✅ Use minimal trusted base images
✅ Use multi-stage builds
✅ Remove unnecessary packages
✅ Keep dependencies updated
✅ Avoid secrets inside images
✅ Run containers as non-root where possible
✅ Scan images regularly
✅ Use immutable image tags in deployments

Instead of:

myapp:latest

prefer an immutable version:

myapp:1.0.5

or:

myapp:<commit-sha>

This makes deployments more reproducible.
☸️ 3. Kubernetes Optimization

Kubernetes should be configured according to application requirements.

Important optimization areas:

Pods
Deployments
Requests/Limits
HPA
Node Capacity
Scheduling
Health Probes
Services
Network Policies
📈 Resource Requests and Limits

Example:

resources:
  requests:
    cpu: "100m"
    memory: "128Mi"

  limits:
    cpu: "500m"
    memory: "512Mi"

Why use them?

Requests help Kubernetes schedule workloads.

Limits prevent a container from consuming unlimited resources.
🔄 Horizontal Pod Autoscaler

HPA can automatically adjust the number of replicas.

Example:

apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler

metadata:
  name: backend-hpa

spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: backend

  minReplicas: 2
  maxReplicas: 10

  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70
❤️ 4. Reliability Improvements

A production application should recover automatically from common failures.

Important Kubernetes features:

✅ Multiple replicas
✅ Readiness probes
✅ Liveness probes
✅ Startup probes where needed
✅ Horizontal Pod Autoscaling
✅ Load balancing
✅ Rolling deployments
✅ Pod disruption controls
✅ Multi-AZ infrastructure where appropriate
🩺 Health Probes

Readiness Probe

Determines whether the application is ready to receive traffic.

readinessProbe:
  httpGet:
    path: /health
    port: 3000

  initialDelaySeconds: 10
  periodSeconds: 10
Liveness Probe

Determines whether the application is still healthy.

livenessProbe:
  httpGet:
    path: /health
    port: 3000

  initialDelaySeconds: 30
  periodSeconds: 20
🔄 Rolling Deployment

Kubernetes can gradually replace old pods.

Old Version
   │
   ├── Pod 1
   ├── Pod 2
   └── Pod 3
        │
        ▼
   New Version
        │
        ├── Pod 1
        ├── Pod 2
        └── Pod 3

This helps reduce downtime during application updates.
🔐 5. Security Optimization

Security should be implemented throughout the DevOps lifecycle.

Plan
 ↓
Code Security
 ↓
Dependency Scan
 ↓
Container Scan
 ↓
IaC Scan
 ↓
Kubernetes Security
 ↓
Runtime Monitoring
🛡️ Security Tools

SonarQube

Used for:

Static analysis

Code quality

Security issues

Code smells

Maintainability analysis

Trivy

Can scan:

Container Images
Filesystems
Dependencies
Infrastructure Configuration

Example:

trivy image myapp:1.0.5

Checkov

Used for Infrastructure as Code scanning.

checkov -d terraform/
☸️ Kubernetes Security Best Practices

✅ Use RBAC
✅ Follow least privilege
✅ Avoid privileged containers
✅ Avoid running as root
✅ Use NetworkPolicies where required
✅ Scan container images
✅ Secure Kubernetes Secrets
✅ Restrict unnecessary external access
✅ Keep cluster components updated
🔑 Secrets Management

Never commit:

AWS Access Keys
Database Passwords
API Tokens
Private Keys
Application Secrets

Use appropriate mechanisms such as:

AWS Secrets Manager
AWS Systems Manager Parameter Store
Kubernetes Secrets
Jenkins Credentials
GitHub Actions Secrets

For production, prefer short-lived credentials and workload identity mechanisms where available.
🏗️ 6. Terraform Optimization

Terraform should remain modular, predictable, and maintainable.

Recommended structure:

terraform/
│
├── main.tf
├── providers.tf
├── variables.tf
├── outputs.tf
├── versions.tf
├── backend.tf
│
└── modules/
    ├── vpc/
    ├── eks/
    ├── security-group/
🧩 Terraform Modules

Instead of repeating resources:

VPC Code
EC2 Code
Security Group Code

create reusable modules:

modules/
├── vpc/
├── eks/
├── rds/
└── security/

Benefits

Reusable
   ↓
Consistent
   ↓
Maintainable
   ↓
Scalable
💰 7. AWS Cost Optimization

Cloud optimization is an important DevOps responsibility.

Common sources of unnecessary cost

Unused EC2 instances
Unused EBS volumes
Unused Elastic IPs
Unused Load Balancers
Oversized instances
Excessive NAT Gateway usage
Unused snapshots
Unused container images
Idle databases
Over-provisioned EKS nodes

💵 Cost Optimization Strategies

✅ Right-size resources
✅ Remove unused resources
✅ Use autoscaling
✅ Monitor AWS Cost Explorer
✅ Set budgets and alerts
✅ Review EKS node capacity
✅ Clean unused images
✅ Optimize storage
✅ Use managed services appropriately

For learning environments:

terraform destroy

can be used when the infrastructure is no longer required.

Always verify what will be destroyed before confirming.
8. Monitoring Optimization

Monitoring should focus on useful, actionable information.

A typical stack:

Application
     │
     ▼
Prometheus
     │
     ▼
Grafana
     │
     ▼
Alertmanager
     │
     ▼
Notification
Key Metrics

Monitor:

CPU Usage
Memory Usage
Disk Usage
Request Rate
Response Time
Error Rate
Pod Restarts
Pod Availability
Database Latency
Network Traffic
Deployment Success Rate
Infrastructure Cost
 Alert Optimization

Bad alert:

CPU = 71%

This may not require immediate action.

Better alert:

CPU > 90%
FOR 10 minutes

combined with meaningful context.

Alert best practices

✅ Alert on symptoms
✅ Define severity
✅ Add useful labels
✅ Include runbook links where possible
✅ Avoid duplicate alerts
✅ Group related alerts
✅ Review noisy alerts
9. Grafana Dashboard

A useful dashboard can include:

┌─────────────────────────────────────────┐
│         APPLICATION OVERVIEW            │
├────────────┬────────────┬───────────────┤
│ CPU Usage  │ Memory     │ Request Rate  │
├────────────┼────────────┼───────────────┤
│ Error Rate │ Latency    │ Pod Status    │
├────────────┼────────────┼───────────────┤
│ Database   │ Network    │ Availability  │
└────────────┴────────────┴───────────────┘

Dashboards should help engineers answer:

Is the application healthy?

Is traffic increasing?

Are errors increasing?

Which service is slow?

Are pods restarting?

Is infrastructure running normally?
10. CI/CD Optimization

The CI/CD pipeline should be fast, reliable, and secure.

Recommended workflow:

Code
 ↓
Build
 ↓
Unit Test
 ↓
SAST
 ↓
Dependency Scan
 ↓
Docker Build
 ↓
Container Scan
 ↓
Push Image
 ↓
Deploy
 ↓
Smoke Test
 ↓
Monitor
Pipeline Optimization

✅ Cache dependencies
✅ Use parallel stages where appropriate
✅ Avoid unnecessary builds
✅ Fail fast on critical checks
✅ Reuse Docker layers
✅ Scan only changed components when appropriate
✅ Use immutable image tags
✅ Automate rollback
✅ Keep pipeline steps simple
Rollback Strategy

A production deployment should have a recovery strategy.

For Kubernetes:

kubectl rollout history deployment/backend

Rollback:

kubectl rollout undo deployment/backend

Check rollout status:

kubectl rollout status deployment/backend

This provides a simple recovery mechanism when a deployment introduces a problem.
11. Container Registry Optimization

Container images can be stored in:

Amazon ECR

Docker Hub

Another approved container registry

Recommended practices:

✅ Use immutable version tags
✅ Remove unused images
✅ Enable vulnerability scanning
✅ Apply lifecycle policies
✅ Avoid unnecessarily large images

Example:

myapp:
  ├── 1.0.0
  ├── 1.0.1
  ├── 1.0.2
  └── <commit-sha>
 12. Scalability

Scalability means the system can handle increasing workload.

Low Traffic
    ↓
2 Pods
    ↓
Medium Traffic
    ↓
4 Pods
    ↓
High Traffic
    ↓
8 Pods

Kubernetes can support this through:

Horizontal Pod Autoscaler
Cluster Autoscaler
Load Balancing
ReplicaSets

The exact scaling strategy should be based on workload behavior and cluster capacity.

13. Reliability and High Availability

A production-like AWS architecture can use:

                AWS Region
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
      Availability         Availability
        Zone A                Zone B
          │                     │
       EKS Node              EKS Node
          │                     │
       Pods                    Pods
          └─────────┬───────────┘
                    │
               Load Balancer

Benefits:

✅ Fault tolerance
✅ Higher availability
✅ Better resilience
✅ Reduced single points of failure
