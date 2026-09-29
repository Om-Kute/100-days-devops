🚨 Day 96/100 – Incident Management & Alerting
Detect • Respond • Resolve • Learn • Prevent

As part of my 100 Days of DevOps journey, Day 96 focuses on Incident Management and Alerting.

Monitoring tells us that something is happening. Incident management provides the process for determining the impact, responding to the issue, restoring service, and learning from the incident.

This topic combines:

Prometheus
Alertmanager
Monitoring
Alert routing
On-call practices
Incident response
Escalation
Runbooks
Post-incident reviews
Reliability metrics
🚨 1. What Is an Incident?

An incident is an event that causes or may cause an interruption, degradation, or unexpected behavior in a service.

Examples:

Application Down
Database Unavailable
High CPU Usage
Memory Exhaustion
API Errors
Network Failure
Deployment Failure
Kubernetes Pod Crash
Cloud Service Failure

Example:

Users
  │
  ▼
Application
  │
  X
Service Failure
  │
  ▼
Monitoring Alert
  │
  ▼
Incident Response

The goal is to restore normal service as quickly and safely as possible while capturing information needed for later analysis
🔍 2. Monitoring vs Incident Management
Monitoring	Incident Management
Detects system conditions	Coordinates response
Collects metrics	Assigns ownership
Creates alerts	Handles escalation
Shows system health	Restores service
Provides visibility	Documents incidents
Identifies anomalies	Drives learning and prevention
Simple idea
Monitoring
    ↓
Something is wrong
    ↓
Alert
    ↓
Incident Management
    ↓
Response
    ↓
Resolution
    ↓
Learning
🔄 3. Incident Management Lifecycle

A typical incident lifecycle is:

        ┌─────────────┐
        │   Detect    │
        └──────┬──────┘
               ↓
        ┌─────────────┐
        │    Triage   │
        └──────┬──────┘
               ↓
        ┌─────────────┐
        │   Respond   │
        └──────┬──────┘
               ↓
        ┌─────────────┐
        │   Resolve   │
        └──────┬──────┘
               ↓
        ┌─────────────┐
        │    Learn    │
        └──────┬──────┘
               ↓
        ┌─────────────┐
        │   Prevent   │
        └─────────────┘
1️⃣ Detect

The monitoring system identifies an abnormal condition.

Examples:

CPU > 90%
Memory > 85%
HTTP 5xx errors increasing
Application unavailable
Pod restarting repeatedly
Disk almost full
2️⃣ Triage

The team determines:

What happened?
Which service is affected?
How many users are affected?
What is the severity?
Who should respond?
Is escalation required?
3️⃣ Respond

The responder investigates and attempts to reduce the impact.

Typical actions:

Check dashboards
Check logs
Check traces
Check recent deployments
Check infrastructure
Rollback if appropriate
Scale resources if appropriate
Restart failed components if appropriate
4️⃣ Resolve

The service is restored to an acceptable operating state.

Examples:

Rollback deployment
Fix configuration
Restore database
Scale infrastructure
Replace failed instance
Correct networking issue
5️⃣ Learn

After the incident:

Review what happened
Identify contributing factors
Document the timeline
Review response effectiveness
Identify gaps in monitoring
6️⃣ Prevent

Implement actions that reduce the likelihood or impact of recurrence.

Examples:

Improve monitoring
Add an alert
Improve automation
Fix application code
Improve capacity planning
Update runbook
Improve deployment process
Strengthen testing
📊 4. Alerting Architecture

A common Prometheus-based alerting architecture:

              ┌──────────────┐
              │ Linux Server │
              │ Node Exporter│
              └──────┬───────┘
                     │
                     │ Metrics
                     ▼
              ┌──────────────┐
              │ Prometheus   │
              │              │
              │ Collect      │
              │ Evaluate     │
              └──────┬───────┘
                     │
                     │ Alerts
                     ▼
              ┌──────────────┐
              │ Alertmanager │
              │              │
              │ Group        │
              │ Route        │
              │ Silence      │
              └──────┬───────┘
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
        Email       Slack    Incident Tool
🔥 5. Prometheus

Prometheus collects and stores time-series metrics and evaluates alerting rules.

Example metric:

node_cpu_seconds_total

Another example:

node_memory_MemAvailable_bytes

Prometheus can evaluate rules such as:

CPU usage > threshold

and send alert notifications to Alertmanager.
