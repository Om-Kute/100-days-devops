🐳 Day 77 – Jenkins + Docker
🎯 Objective
Integrate Jenkins with Docker to automatically build Docker images as part of a CI/CD pipeline and push versioned images to a container registry.
🔗 Jenkins + Docker
Jenkins can automate Docker image creation after source code is pushed to GitHub.
Developer
    │
    ▼
  GitHub
    │
    ▼
  Jenkins
    │
    ├── Checkout
    ├── Build
    ├── Test
    └── Docker Build
          │
          ▼
      Docker Image
          │
          ▼
     Docker Registry
🎯 Goal
The main goal is to automate:
Code Push
    ↓
Jenkins Trigger
    ↓
Build Application
    ↓
Run Tests
    ↓
Build Docker Image
    ↓
Tag Image
    ↓
Push Image
    ↓
Docker Registry
🐳 What is Docker?
Docker is a containerization platform that packages an application and its dependencies into a container image.
Application
     +
Dependencies
     +
Configuration
     ↓
Docker Image
     ↓
Container
