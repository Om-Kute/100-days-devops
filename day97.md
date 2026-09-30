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
🔍 Common Security Risks

DevOps environments can face many types of security risks.

1. Insecure Code

Examples:

SQL Injection
Command Injection
XSS
Insecure authentication
Authorization flaws
2. Vulnerable Dependencies

Applications often depend on third-party libraries.

An outdated dependency may contain known vulnerabilities.

Example:

Application
    ↓
Dependency A
    ↓
Dependency B
    ↓
Vulnerable Library

Dependency scanning can help identify known vulnerable packages.

3. Exposed Secrets

Never commit:

❌ AWS Access Keys
❌ Passwords
❌ API Tokens
❌ Private Keys
❌ Database Credentials

Avoid:

AWS_ACCESS_KEY = "MY_SECRET_KEY"

Use secure secret-management mechanisms instead.

4. Insecure Containers

Container risks can include:

Vulnerable base images
Unnecessary packages
Running as root
Exposed ports
Embedded secrets
Outdated dependencies
5. Misconfigured Infrastructure

Examples:

Public S3 bucket
Open security group
Excessive IAM permissions
Public database
Unrestricted network access

Infrastructure as Code scanning can identify many configuration problems before deployment.
🛠️ DevSecOps Tools

Common tools include:

Tool	Primary Use
SonarQube	Code quality and static analysis
Trivy	Vulnerability scanning
OWASP ZAP	Dynamic application security testing
Checkov	IaC security scanning
kube-bench	Kubernetes security checks
GitHub Dependabot	Dependency updates/alerts
Semgrep	Static code analysis
Gitleaks	Secret detection

Tool selection depends on the language, platform, pipeline, and security requirements.

🔎 SAST
Static Application Security Testing

SAST analyzes source code or compiled representations without executing the application.

Example workflow:

Source Code
     ↓
SAST Scanner
     ↓
Security Findings
     ↓
Developer Fix
     ↓
Build

Examples:

SonarQube
Semgrep
CodeQL

SAST is useful for finding issues early in development.
🌐 DAST
Dynamic Application Security Testing

DAST tests a running application from the outside.

Running Application
        ↑
        │
   DAST Scanner
        │
        ↓
Security Findings

Example:

OWASP ZAP

DAST can help identify vulnerabilities that are observable in a running application.

📦 Dependency Scanning

Dependency scanning checks application libraries and packages for known vulnerabilities.

Example:

Application
     ↓
package.json / requirements.txt / pom.xml
     ↓
Dependency Scanner
     ↓
Known Vulnerabilities

Examples:

npm audit
pip-audit
Dependabot
Trivy
🐳 Container Security

Containers should be scanned before deployment.

Example:

trivy image nginx:latest

A typical workflow:

Dockerfile
    ↓
docker build
    ↓
Container Image
    ↓
Trivy Scan
    ↓
Security Check
    ↓
Registry
    ↓
Deployment
🧱 Docker Security Best Practices
✅ Use trusted base images
✅ Keep images updated
✅ Use minimal images
✅ Scan images regularly
✅ Avoid running containers as root
✅ Do not embed secrets
✅ Remove unnecessary packages
✅ Pin important dependencies
✅ Limit container privileges
☸️ Kubernetes Security

Kubernetes environments require security at multiple layers.

Important areas include:

RBAC
Network Policies
Pod Security
Secrets management
Admission controls
Image scanning
Namespace isolation
Resource limits
API server security

Example:

Kubernetes Cluster
        │
 ┌──────┼────────┐
 ↓      ↓        ↓
RBAC  Network   Pod
      Policy   Security
