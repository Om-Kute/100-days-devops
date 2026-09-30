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
🚀 Shift-Left Security

Shift Left means moving security activities earlier in the development lifecycle.

Traditional
Code → Build → Test → Deploy → Security
Shift Left
Security
   ↓
Plan → Code → Build → Test → Deploy

The earlier a vulnerability is discovered, the earlier the team can investigate and fix it.

💡 Why DevSecOps?

Without security automation:

Developer
    ↓
Code
    ↓
Build
    ↓
Deploy
    ↓
Security Issue
    ↓
Manual Investigation

With DevSecOps:

Developer
    ↓
Code
    ↓
Automated Security Scan
    ↓
Vulnerability Found
    ↓
Fix
    ↓
Build
    ↓
Deploy
Benefits
Earlier vulnerability detection
Reduced security risk
Automated security checks
Faster remediation
Better collaboration
Improved compliance readiness
More secure deployments
Better visibility
