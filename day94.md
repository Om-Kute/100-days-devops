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
.

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
