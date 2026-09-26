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
📈 4. PromQL Rate Functions

For counters, rate() is commonly used to calculate the average per-second increase over a time window.

Example:

rate(http_requests_total[5m])

This calculates the average request rate over the last five minutes.

🔢 5. Increase Function

increase() calculates the total increase in a counter over a time range.

Example:

increase(http_requests_total[1h])

This can show the increase in HTTP requests during the las
📊 6. Aggregation in PromQL

PromQL supports aggregation.

Example:

sum(rate(http_requests_total[5m]))

This calculates the total request rate across the selected series.

Another example:

sum by (instance) (rate(http_requests_total[5m]))

This groups request rates by instance.

🐳 7. Container CPU Monitoring

For container environments, cAdvisor metrics can be queried.

Example:

rate(container_cpu_usage_seconds_total[5m])

A more useful aggregation may be:

sum by (container) (
  rate(container_cpu_usage_seconds_total[5m])
)

The exact labels available depend on the cAdvisor and Prometheus setup.
☸️ 8. Kubernetes Monitoring

Kubernetes environments can be monitored using tools such as:

Prometheus
Node Exporter
kube-state-metrics
cAdvisor/container metrics
Alertmanager
Grafana

Example metric:

kube_pod_status_phase

This can be used to inspect Kubernetes Pod phase information.

🚨 9. Prometheus Alerting Rules

Prometheus can evaluate alerting rules.

Example:

groups:
  - name: system-alerts

    rules:
      - alert: HighCPUUsage

        expr: |
          100 - (
            avg by (instance) (
              rate(node_cpu_seconds_total{
                mode="idle"
              }[5m])
            ) * 100
          ) > 80

        for: 5m

        labels:
          severity: warning

        annotations:
          summary: "High CPU usage detected"
          description: "CPU usage has remained above 80% for 5 minutes."
⏱️ 10. The for Duration

The for field prevents temporary spikes from immediately generating alerts.

Example:

for: 5m

This means the alert condition must remain true for the configured duration before the alert becomes firing.

Without an appropriate duration:

Short spike
    ↓
Alert
    ↓
Noise

With a duration:

Short spike
    ↓
Condition disappears
    ↓
No alert
🚦 11. Alert States

Prometheus alerts commonly move through states such as:

Inactive
    │
    │ Condition becomes true
    ▼
Pending
    │
    │ Condition remains true
    ▼
Firing
    │
    │ Condition becomes false
    ▼
Resolved
Inactive

The alert condition is not currently true.

Pending

The condition is true but the configured for duration has not completed.

Firing

The condition has remained true for the required duration.

Resolved

The condition is no longer true.
📡 12. Alertmanager

Alertmanager receives alerts from Prometheus and manages notification delivery.

It supports concepts such as:

Grouping
Routing
Silencing
Inhibition
Notification receivers

Architecture:

Prometheus
    │
    │ Alerts
    ▼
Alertmanager
    │
    ├── Email
    ├── Slack
    ├── Microsoft Teams
    ├── PagerDuty
    └── Webhook
⚙️ 13. Alertmanager Configuration

Basic example:

global:
  resolve_timeout: 5m

route:
  group_by:
    - alertname

  group_wait: 10s
  group_interval: 5m
  repeat_interval: 1h

  receiver: team-alerts

receivers:
  - name: team-alerts

Additional notification configuration depends on the integration being used.

Sensitive credentials should never be committed directly into a public repository.
📦 14. Alert Grouping

Suppose several servers experience the same issue:

Server 1 → High CPU
Server 2 → High CPU
Server 3 → High CPU
Server 4 → High CPU

Without grouping:

Alert
Alert
Alert
Alert

With grouping:

HighCPUUsage
    │
    └── 4 affected instances

Grouping reduces notification noise.

🔇 15. Alert Silencing

Sometimes an alert is expected during maintenance.

Instead of receiving notifications during planned maintenance, an alert can be silenced.

Example scenario:

Scheduled Maintenance
        │
        ▼
Create Silence
        │
        ▼
Expected Alerts
        │
        ▼
No Notifications

After maintenance:

Remove / Expire Silence

Silencing should be controlled carefully so real incidents are not hidden.
🚫 16. Alert Inhibition

Inhibition prevents lower-priority alerts from creating additional noise when a higher-level problem is already known.

Example:

Database Down
      │
      ├── Application Errors
      ├── API Errors
      └── User Requests Failing

Instead of sending many secondary notifications, an inhibition rule can suppress alerts that are consequences of the primary incident.

📊 17. Grafana Alerting

Grafana can visualize metrics and create alert rules depending on the configured data sources and Grafana version.

A typical process:

Grafana
   │
   ▼
Create Panel
   │
   ▼
Choose Query
   │
   ▼
Set Threshold
   │
   ▼
Configure Evaluation
   │
   ▼
Configure Notification
   │
   ▼
Save Alert Rule

Example:

CPU Usage > 80%
for 5 minutes
        ↓
Alert
📈 18. Useful Dashboard Panels

A production dashboard can contain:

┌─────────────────────────────────────────┐
│          SYSTEM OVERVIEW                │
├─────────────────────────────────────────┤
│ CPU Usage       │ Memory Usage          │
│     72%         │      65%              │
├─────────────────┼───────────────────────┤
│ Disk Usage      │ Network Traffic       │
│     58%         │     120 MB/s          │
├─────────────────┼───────────────────────┤
│ Request Rate    │ Error Rate            │
│    1.2K/s       │       0.4%            │
├─────────────────┼───────────────────────┤
│ Latency         │ Active Alerts         │
│    120 ms       │         2             │
└─────────────────────────────────────────┘
🔔 19. Notification Channels

Common notification destinations include:

📧 Email
💬 Slack
💬 Microsoft Teams
🚨 PagerDuty
🔗 Webhooks

The correct notification channel depends on incident severity and team requirements.
