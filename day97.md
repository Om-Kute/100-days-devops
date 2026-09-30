🔐 Day 97/100 – DevSecOps
🛡️ Security in the DevOps Lifecycle

Day 97 focuses on DevSecOps — Development, Security, and Operations.

DevSecOps integrates security practices into the complete software delivery lifecycle instead of treating security as a final step before production.

The core idea is:

Plan → Code → Build → Test → Scan → Deploy → Monitor

Security becomes a shared responsibility between development, security, and operations teams.
🤔 What is DevSecOps?

DevSecOps is the practice of integrating security throughout the DevOps lifecycle.

Traditional approach:

Development
     ↓
Testing
     ↓
Deployment
     ↓
Security Review
     ↓
Production

DevSecOps approach:

        Security
           ↓
Plan → Code → Build → Test → Deploy → Monitor
  ↓      ↓      ↓      ↓       ↓        ↓
Threat  SAST   Scan   DAST   Policy   Runtime
Model   Secrets Dependencies   IaC      Security

Security checks are performed continuously rather than waiting until the end.
🔄 DevSecOps Lifecycle
┌──────────┐
│   PLAN   │
│ Threat   │
│ Modeling │
└────┬─────┘
     ↓
┌──────────┐
│   CODE   │
│ SAST     │
│ Secrets  │
│ Review   │
└────┬─────┘
     ↓
┌──────────┐
│  BUILD   │
│ Dependency│
│ Scanning │
└────┬─────┘
     ↓
┌──────────┐
│   TEST   │
│ DAST     │
│ Security │
│ Testing  │
└────┬─────┘
     ↓
┌──────────┐
│   SCAN   │
│ Container│
│ IaC      │
│ Images   │
└────┬─────┘
     ↓
┌──────────┐
│  DEPLOY  │
│ Policy   │
│ Checks   │
└────┬─────┘
     ↓
┌──────────┐
│ MONITOR  │
│ Runtime  │
│ Security │
└──────────┘
