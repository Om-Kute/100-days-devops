🚀 Day 92/100 – Advanced Monitoring & Alerting
📊 Prometheus • PromQL • Alertmanager • Grafana

Day 92 focuses on Advanced Monitoring & Alerting, building on the monitoring and observability concepts covered on Day 91.

The goal is to move from simply collecting metrics to creating actionable alerts that help DevOps engineers detect problems, investigate incidents, and maintain reliable infrastructure.
🔄 Advanced Monitoring Workflow
                    Metrics
                       │
                       ▼
                ┌─────────────┐
                │ Prometheus  │
                │ Collect     │
                │ Store       │
                │ Evaluate    │
                └──────┬──────┘
                       │
                       ▼
                    PromQL
                       │
                       ▼
                 Alert Rules
                       │
                       ▼
                ┌─────────────┐
                │ Alertmanager│
                └──────┬──────┘
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
        Email        Slack       Webhook
                       │
                       ▼
                  Engineer
                       │
                       ▼
                  Investigate
                       │
                       ▼
                  Fix & Improve
🔭 1. What is Advanced Monitoring?

Basic monitoring answers questions such as:

Is the server running?
Is CPU high?
Is memory available?
Is the service up?

Advanced monitoring goes further:

Why is CPU increasing?
Which service is causing the problem?
How long has the issue existed?
How many users are affected?
Is the problem isolated or widespread?
What should happen when the threshold is exceeded?

Advanced monitoring combines:

Metrics
+
Queries
+
Dashboards
+
Alert Rules
+
Notifications
+
Incident Response
🔥 2. Prometheus

Prometheus is an open-source monitoring and alerting toolkit that collects and stores time-series metrics.

It can:

Scrape metrics
Store time-series data
Query metrics using PromQL
Evaluate alerting rules
Send alerts to Alertmanager
Monitor infrastructure
Monitor applications
Monitor containers
Monitor Kubernetes

Architecture:

Exporter / Application
        │
        │ /metrics
        ▼
   ┌────────────┐
   │ Prometheus │
   └─────┬──────┘
         │
    ┌────┴─────┐
    ▼          ▼
  PromQL     Alerts
    │          │
    ▼          ▼
 Grafana   Alertmanager
🧮 3. PromQL

PromQL (Prometheus Query Language) is used to query and analyze Prometheus time-series data.

Basic Query
up

This can be used to check whether monitored targets are reporting as available.

CPU Metric
node_cpu_seconds_total

This exposes cumulative CPU time by CPU mode.

Memory Metric
node_memory_MemAvailable_bytes

Shows available memory reported by Node Exporter.

Filesystem Metric
node_filesystem_avail_bytes

Shows available filesystem space.
