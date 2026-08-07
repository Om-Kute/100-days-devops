⚖️ Day 46 – AWS Load Balancer & Auto Scaling
🎯 Objective

Learn how AWS distributes application traffic and automatically scales compute resources using Elastic Load Balancing (ELB) and Auto Scaling.
⚖️ What is Elastic Load Balancing?

Elastic Load Balancing automatically distributes incoming application traffic across multiple EC2 instances.

Benefits
High Availability
Fault Tolerance
Better Performance
Scalability
Reduced Downtime
🔀 Types of AWS Load Balancers
1️⃣ Application Load Balancer (ALB)

Layer: 7 (Application Layer)

Supports:

HTTP
HTTPS
WebSocket

Features:

Path-based routing
Host-based routing
SSL termination
Target Groups

Best for:

Web Applications
REST APIs
Microservices

2️⃣ Network Load Balancer (NLB)

Layer: 4 (Transport Layer)

Supports:

TCP
UDP
TLS

Features:

Very low latency
Millions of requests per second
Static IP support

Best for:

High-performance applications
Gaming
Financial systems
