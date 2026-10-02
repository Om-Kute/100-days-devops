🚀 Day 94/100 – Application Performance Monitoring & Distributed Tracing
📊 APM, Distributed Tracing & OpenTelemetry

Day 94 of my 100 Days of DevOps journey focuses on Application Performance Monitoring (APM) and Distributed Tracing.
Modern applications are often built using microservices, APIs, databases, containers, and external services. A single user request may travel through multiple components before returning a response.

Distributed tracing helps us understand this complete request journey and identify:

Slow services
High latency
Failed requests
Database bottlenecks
External API delays
Service dependencies
Performance issues

🔍 1. What is APM?

Application Performance Monitoring (APM) is the practice of monitoring application performance and availability.

APM helps teams understand:

Application Performance
        │
        ├── Response Time
        ├── Error Rate
        ├── Throughput
        ├── Resource Usage
        └── User Experience

Typical APM signals include:

Request latency
HTTP error rate
Requests per second
Database query duration
CPU usage
Memory usage
🧭 2. What is Distributed Tracing?

Distributed tracing tracks a request as it travels through multiple services.

For example:

User
 │
 ▼
API Gateway
 │
 ▼
Order Service
 │
 ▼
Payment Service
 │
 ▼
Database
 │
 ▼
Response

A trace records this entire journey.

Without tracing, finding the slow component in a microservices system can be difficult.
🧩 3. Trace vs Span
Trace

A trace represents the complete journey of a request.

Example:

Trace ID: abc123

The trace may contain multiple spans.

Span

A span represents one operation or unit of work within a trace.

Example:

Trace
 │
 ├── API Gateway       120 ms
 ├── Order Service     250 ms
 ├── Payment Service   400 ms
 └── Database          180 ms

The total trace gives an end-to-end view, while each span provides detailed information about an individual operation.
🆔 4. Trace ID and Span ID
Trace ID

A unique identifier associated with the overall request.

Trace ID:
9f2a7c8d...
Span ID

A unique identifier for an individual operation.

Span ID:
a82c91...

Conceptually:

Trace ID
   │
   ├── Span A
   │
   ├── Span B
   │
   ├── Span C
   │
   └── Span D

This allows engineers to connect operations belonging to the same request.
🔗 5. Context Propagation

Context propagation allows trace information to travel from one service to another.

Example:

Service A
   │
   │ Trace Context
   ▼
Service B
   │
   │ Trace Context
   ▼
Service C

The receiving service can continue the same trace instead of starting an unrelated trace.

In HTTP-based systems, trace context is commonly propagated through headers.

🌐 6. Distributed Tracing Example

Consider an e-commerce application.

                 User
                   │
                   ▼
             API Gateway
                   │
          ┌────────┴────────┐
          ▼                 ▼
    Order Service      User Service
          │
          ▼
    Payment Service
          │
          ▼
       Database

A single request could produce:

Trace: order-service

API Gateway       120 ms
Order Service     250 ms
Payment Service   400 ms
Database          180 ms
External API      100 ms

If the request takes 1 second, tracing helps identify which components contributed most to the latency.
🛰️ 7. OpenTelemetry

OpenTelemetry (OTel) is an open-source observability framework for generating, collecting, and exporting telemetry data.

It supports:

Metrics
Logs
Traces

Architecture:

Application
    │
    ▼
OpenTelemetry Instrumentation
    │
    ▼
OpenTelemetry Collector
    │
    ├─────────────┬──────────────┐
    ▼             ▼              ▼
  Traces        Metrics         Logs
    │             │              │
    ▼             ▼              ▼
  Jaeger       Prometheus        Loki
    │             │              │
    └─────────────┴──────────────┘
                   │
                   ▼
                Grafana

OpenTelemetry can send telemetry to different compatible backends
🧰 8. OpenTelemetry Components

A typical OpenTelemetry setup can include:

Instrumentation

Collects telemetry from applications.

SDK

Processes telemetry inside the application.

Collector

Receives, processes, and exports telemetry.

Exporters

Send telemetry to supported backends.

Example:

Application
     ↓
OpenTelemetry SDK
     ↓
OTel Collector
     ↓
Jaeger / Tempo / Prometheus / Loki
🔥 9. Jaeger

Jaeger is a distributed tracing platform.

It can be used to:

Store traces
Search traces
Visualize spans
Analyze request latency
Find failed operations
Understand service dependencies

Conceptually:

Application
     │
     ▼
OpenTelemetry
     │
     ▼
   Jaeger
     │
     ▼
Trace Visualization
🟠 10. Grafana Tempo

Grafana Tempo is a distributed tracing backend designed to integrate with the Grafana observability ecosystem.

Example:

Application
     │
     ▼
OpenTelemetry
     │
     ▼
    Tempo
     │
     ▼
   Grafana

Tempo can be used alongside metrics and logs to create a more complete observability workflow.

📊 11. Grafana

Grafana provides visualization and dashboards.

It can display:

Metrics
Logs
Traces
Alerts

Example:

                 Grafana
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
     Metrics       Logs       Traces
        │           │           │
   Prometheus      Loki      Tempo/Jaeger

This allows engineers to investigate incidents using multiple telemetry signals.

📈 12. Important APM Metrics
Latency

Measures how long an operation takes.

Example:

API Response Time = 250 ms
Throughput

Measures how many requests are processed over time.

Example:

Requests = 500 req/sec
Error Rate

Measures failed requests.

Example:

HTTP 5xx Errors = 2%
Saturation

Shows how heavily a resource is being used.

Examples:

CPU = 85%
Memory = 90%
Disk = 78%
Apdex / User Experience

Apdex is one approach for representing user satisfaction based on response-
13. Metrics + Logs + Traces

Modern observability commonly combines three major telemetry signals.

             Observability
                   │
       ┌───────────┼───────────┐
       ▼           ▼           ▼
    Metrics       Logs       Traces
       │           │           │
       ▼           ▼           ▼
  Performance   Events    Request Flow
Metrics

Tell you what is happening.

Logs

Tell you what events occurred.

Traces

Help explain where a request traveled and where time was spent.

Together they provide stronger troubleshooting context.
14. Complete Tracing Architecture
┌───────────────────────┐
│     User Request      │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│     API Gateway       │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│    Order Service      │
│   OpenTelemetry SDK   │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│   Payment Service     │
│   OpenTelemetry SDK   │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│       Database        │
└───────────────────────┘
            │
            │ Telemetry
            ▼
┌───────────────────────┐
│ OpenTelemetry         │
│ Collector             │
└───────────┬───────────┘
            │
      ┌─────┴─────┐
      ▼           ▼
   Jaeger        Tempo
      │           │
      └─────┬─────┘
            ▼
         Grafana
15. Example Trace

Suppose a customer places an order.

Trace ID: 8a7f91c2

0 ms
 │
 ├── API Gateway
 │     └── 120 ms
 │
 ├──── Order Service
 │       └── 250 ms
 │
 ├──────── Payment Service
 │           └── 400 ms
 │
 ├──────────── Database
 │               └── 180 ms
 │
 └──────────────── External API
                     └── 100 ms

A trace visualization can make the slow portion immediately visible.
16. Alerting Strategy

Monitoring becomes more useful when alerts are meaningful and actionable.

A good alerting workflow is:

Metric
  ↓
Threshold / Condition
  ↓
Alert Rule
  ↓
Alertmanager
  ↓
Notification
  ↓
Engineer / Team
  ↓
Investigation

Examples:

High API latency
High error rate
Service unavailable
CPU saturation
Memory pressure
Database connection failures
17. Managing Notifications Effectively

Too many alerts can cause alert fatigue.

A practical notification strategy is:

                    Alerts
                      │
             ┌────────┴────────┐
             ▼                 ▼
          Critical           Warning
             │                 │
             ▼                 ▼
        Immediate          Review Soon
        Notification
Good practices
Set meaningful thresholds
Prioritize alerts by severity
Avoid duplicate notifications
Group related alerts
Route alerts to the appropriate team
Use escalation policies
Suppress known maintenance alerts
Regularly review noisy alerts
Make alerts actionable

The goal is:

Notify quickly when action is required, without overwhelming engineers with unnecessary notifications.
 18. Useful Commands & Examples
Send a request with trace context
curl -H "traceparent: ..." http://localhost:8080/api/orders

The exact traceparent value should come from a valid tracing context rather than being copied arbitrarily.

View Kubernetes application logs
kubectl logs <pod-name>
Follow Kubernetes logs
kubectl logs -f <pod-name>
Check Kubernetes pods
kubectl get pods
Inspect a pod
kubectl describe pod <pod-name>
Check Prometheus targets
http://<prometheus-host>:9090/targets
View Grafana
http://<grafana-host>:3000
19. Monitoring Docker Applications

For containerized workloads, container-level metrics can be collected using tools such as cAdvisor.

Architecture:

Docker Containers
       │
       ▼
    cAdvisor
       │
       ▼
   Prometheus
       │
       ▼
    Grafana

Useful container metrics include:

CPU usage
Memory usage
Network traffic
Container restarts
Filesystem usage
20. Monitoring Kubernetes

Observability becomes especially important in Kubernetes because applications may contain many dynamically scheduled workloads.

Typical stack:

Kubernetes
    │
    ├── Application Metrics
    ├── Node Metrics
    ├── Container Metrics
    ├── Logs
    └── Traces
           │
           ▼
      Observability
           │
     ┌─────┼─────┐
     ▼     ▼     ▼
 Metrics  Logs  Traces

Tracing can help investigate:

Slow APIs
Service-to-service latency
Failed requests
Dependency problems
Database delays
21. Troubleshooting with Traces

Suppose users report that checkout is slow.

Without tracing:

Checkout is slow
       ↓
Check everything manually

With tracing:

Checkout Request
      ↓
API Gateway       100 ms
      ↓
Order Service     150 ms
      ↓
Payment Service   900 ms  ← Bottleneck
      ↓
Database          100 ms

The trace immediately points toward the payment service for deeper investigation.


  
Strong for known failure modes	Strong for complex distributed systems

Both are complementary rather than competing concepts.
