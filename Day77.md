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
🤖 Why Jenkins + Docker?
Jenkins automates the CI/CD workflow, while Docker provides a consistent packaging format for applications.
Together:
GitHub
   ↓
Jenkins
   ↓
Build
   ↓
Test
   ↓
Docker Build
   ↓
Docker Image
   ↓
Registry
This creates a repeatable container build process.
🏗️ Architecture
Developer
                        │
                        ▼
                 GitHub Repository
                        │
                     Webhook
                        │
                        ▼
                Jenkins Controller
                        │
                        ▼
                    Jenkins Agent
                        │
              ┌─────────┴─────────┐
              ▼                   ▼
         Application Build     Docker Build
                                    │
                                    ▼
                              Docker Image
                                    │
                                    ▼
                              Docker Registry
📄 Dockerfile
A Dockerfile defines how a Docker image is built.
Example for a Java application:
FROM eclipse-temurin:21-jre

WORKDIR /app

COPY target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
The exact base image and Java version should match your application's requirements.
🔨 Docker Build
Build the image:
docker build -t myapp:1.0 .
Explanation:
docker build
     ↓
Reads Dockerfile
     ↓
Builds Image
     ↓
myapp:1.0
