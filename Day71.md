🚀 Day 71 – CI/CD Fundamentals
🎯 Objective
Understand the fundamentals of CI/CD, why automation is important in DevOps, and how source code moves from a developer's commit to a deployed application.
🔄 What is CI/CD?
CI/CD is a set of practices and automation techniques used to continuously integrate, test, deliver, and deploy software.
The basic idea is:
Code
  ↓
Build
  ↓
Test
  ↓
Package
  ↓
Deploy
  ↓
Release
  ↓
Monitor
The goal is to deliver software faster, more reliably, and with fewer manual errors.
🔵 Continuous Integration (CI)
Continuous Integration is the practice of frequently integrating code changes into a shared repository and automatically validating those changes.
Developer
    ↓
Git Commit
    ↓
GitHub
    ↓
CI Pipeline
    ↓
Build
    ↓
Automated Tests
    ↓
Feedback
CI focuses on:
Frequent code integration
Automated builds
Automated testing
Early bug detection
Fast developer feedback
🟢 Continuous Delivery
Continuous Delivery automatically builds, tests, and prepares software so that it is always ready for release.
A production release may still require manual approval.
Code
 ↓
Build
 ↓
Test
 ↓
Package
 ↓
Staging
 ↓
Manual Approval
 ↓
Production
🟠 Continuous Deployment
Continuous Deployment goes one step further.
Validated changes are automatically deployed to production without a manual approval step.
Code
 ↓
Build
 ↓
Test
 ↓
Package
 ↓
Deploy
 ↓
Production
⚖️ CI vs Continuous Delivery vs Continuous Deployment
Concept
Main Purpose
Production Deployment
Continuous Integration
Integrate and test code frequently
No
Continuous Delivery
Keep software ready for release
Usually manual approval
Continuous Deployment
Automatically release validated changes
Automatic
Easy Memory Trick
CI → Integrate & Test
CD → Deliver & Release
Continuous Deployment → Automatically Deploy
🏗️ CI/CD Pipeline
A typical CI/CD pipeline looks like:
Developer
                  │
                  ▼
               Git Push
                  │
                  ▼
                Build
                  │
                  ▼
                Test
                  │
                  ▼
               Package
                  │
                  ▼
               Deploy
                  │
                  ▼
               Release
                  │
                  ▼
               Monitor
🔧 CI/CD Pipeline Stages
1. Code
Developer writes and commits application code.
git add .
git commit -m "Add new feature"
git push
2. Build
The application is compiled or packaged.
Examples:
mvn package
or:
npm install
npm run build
3. Test
Automated tests validate the application.
Examples:
Unit tests
Integration tests
API tests
End-to-end tests
Example:
mvn test
4. Package
The application is packaged for deployment.
Examples:
JAR
WAR
Docker Image
ZIP
Binary
For Docker:
docker build -t myapp:1.0 .
5. Deploy
Deploy the application to an environment.
Examples:
Development
     ↓
Testing
     ↓
Staging
     ↓
Production
6. Release
The validated application is released to users.
7. Monitor
After deployment, monitor:
Application health
Logs
Errors
Performance
Availability
Infrastructure
User impact
♾️ DevOps Lifecycle
CI/CD is part of the broader DevOps lifecycle.
PLAN
          ↓
        CODE
          ↓
        BUILD
          ↓
        TEST
          ↓
       RELEASE
          ↓
       DEPLOY
          ↓
       OPERATE
          ↓
       MONITOR
          │
          └──────────────► PLAN
DevOps encourages continuous feedback and improvement throughout this lifecycle.
🚀 Why CI/CD is Important
CI/CD helps organizations:
Release software faster
Detect bugs earlier
Reduce manual work
Improve consistency
Reduce deployment risk
Increase developer productivity
Standardize deployment processes
Enable frequent releases
Improve feedback loops
🧰 Popular CI/CD Tools
Some commonly used tools include:
Jenkins
GitHub Actions
GitLab CI/CD
CircleCI
Azure Pipelines
Bamboo
Argo CD
In this learning phase, the primary focus will be Jenkins.
🔗 Example DevOps Pipeline
A modern application could use:
GitHub
   │
   ▼
Jenkins
   │
   ▼
Build
   │
   ▼
Test
   │
   ▼
Docker Build
   │
   ▼
Docker Registry
   │
   ▼
Kubernetes
   │
   ▼
Application
   │
   ▼
Monitoring
This connects the technologies learned earlier in the 100 Days of DevOps journey.
🐳 CI/CD + Docker
Docker makes applications easier to package consistently.
Example:
docker build -t myapp:1.0 .
Then the CI/CD pipeline can push the image to a registry:
docker push username/myapp:1.0
Later, Kubernetes can deploy that image.
Source Code
    ↓
CI/CD
    ↓
Docker Image
    ↓
Registry
    ↓
Kubernetes
