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
☁️ LoadBalancer

LoadBalancer exposes a Service through an external load balancer when supported by the Kubernetes environment.

Example:

apiVersion: v1
kind: Service

metadata:
  name: web-service

spec:
  type: LoadBalancer

  selector:
    app: web

  ports:
    - port: 80
      targetPort: 8080

Architecture:

Internet
   │
   ▼
Cloud Load Balancer
   │
   ▼
Service
   │
   ▼
Pods
🔀 Service Types Comparison
Service Type	Main Purpose
ClusterIP	Internal cluster access
NodePort	Expose Service through node ports
LoadBalancer	External load balancer integration
ExternalName	Maps a Service name to an external DNS name
🚪 What is Ingress?

An Ingress is a Kubernetes API resource used to define rules for routing HTTP/HTTPS traffic to Services.

It can provide:

Host-based routing
Path-based routing
TLS termination
Centralized HTTP/HTTPS routing
Internet
    │
    ▼
 Ingress
    │
 ┌──┴──┐
 ▼     ▼
Service A   Service B
 │            │
 ▼            ▼
Pods         Pods
⚙️ Ingress Controller

An Ingress resource only defines routing rules.

An Ingress Controller is responsible for implementing those rules.

Ingress Resource
      │
      ▼
Ingress Controller
      │
      ▼
Kubernetes Services
      │
      ▼
Pods

Examples of Ingress Controller implementations include:

NGINX Ingress Controller
Traefik
HAProxy
Cloud-provider-specific controllers

The exact controller and configuration depend on the Kubernetes distribution and environment.

🏗️ Ingress Architecture
                   Internet
                      │
                      ▼
               Ingress Controller
                      │
               ┌──────┴──────┐
               ▼             ▼
          Service A      Service B
               │             │
               ▼             ▼
             Pods           Pods
🌍 Host-Based Routing

Host-based routing routes traffic according to the requested hostname.

Example:

app.example.com
       │
       ▼
   Service A

api.example.com
       │
       ▼
   Service B

Example:

apiVersion: networking.k8s.io/v1
kind: Ingress

metadata:
  name: host-routing

spec:
  rules:

    - host: app.example.com

      http:
        paths:
          - path: /
            pathType: Prefix

            backend:
              service:
                name: app-service
                port:
                  number: 80

    - host: api.example.com

      http:
        paths:
          - path: /
            pathType: Prefix

            backend:
              service:
                name: api-service
                port:
                  number: 80
🛣️ Path-Based Routing

Path-based routing uses the URL path to select the backend Service.

Example:

example.com/app
      │
      ▼
App Service

example.com/api
      │
      ▼
API Service

Example:

apiVersion: networking.k8s.io/v1
kind: Ingress

metadata:
  name: path-routing

spec:
  rules:

    - host: example.com

      http:
        paths:

          - path: /app
            pathType: Prefix

            backend:
              service:
                name: app-service
                port:
                  number: 80

          - path: /api
            pathType: Prefix

            backend:
              service:
                name: api-service
                port:
                  number: 80
🔐 TLS / HTTPS with Ingress

Ingress can be configured to terminate TLS for HTTPS traffic.

Example:

apiVersion: networking.k8s.io/v1
kind: Ingress

metadata:
  name: secure-ingress

spec:

  tls:
    - hosts:
        - secure.example.com
      secretName: tls-secret

  rules:

    - host: secure.example.com

      http:
        paths:

          - path: /
            pathType: Prefix

            backend:
              service:
                name: web-service
                port:
                  number: 80

Architecture:

HTTPS Client
     │
     ▼
TLS Termination
     │
     ▼
Ingress Controller
     │
     ▼
Service
     │
     ▼
Pods
