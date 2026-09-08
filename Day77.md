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
📋 List Docker Images
docker images
or:
docker image ls
Example:
REPOSITORY    TAG       IMAGE ID
🏷️ Docker Image Tagging
Before pushing an image to Docker Hub, tag it with the registry repository name.
Example:
docker tag myapp:1.0 USERNAME/myapp:1.0
Verify:
docker images
Concept:
myapp:1.0
    │
    ▼
USERNAME/myapp:1.0
🔐 Jenkins Credentials
Jenkins should manage Docker registry credentials securely.
Go to:
Jenkins Dashboard
      ↓
Manage Jenkins
      ↓
Credentials
      ↓
Add Credentials
For Docker Hub, use an appropriate credential type and preferably a Docker Hub access token rather than a reusable account password.
Example credential ID:
dockerhub-credentials
⚠️ Never Hardcode Credentials
Avoid:
sh 'docker login -u admin -p mypassword'
Do not commit passwords or tokens to GitHub.
Prefer Jenkins-managed credentials:
Jenkins Credentials
        ↓
Secure Binding
        ↓
Pipeline
        ↓
Docker Registry
🔑 Docker Login
For a manual test, Docker can authenticate interactively:
docker login
For automation, use Jenkins Credentials and avoid exposing secrets in command output.
📤 Docker Push
After tagging:
docker push USERNAME/myapp:1.0
Workflow:
Docker Image
     ↓
Tag
     ↓
Docker Registry
     ↓
Push
🔄 Jenkins + Docker Pipeline
A basic Pipeline can look like:
pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t myapp:${BUILD_NUMBER} .'
            }
        }
    }

    post {
        success {
            echo 'Docker image build completed successfully'
        }

        failure {
            echo 'Pipeline failed'
        }
    }
}
checkout scm is useful when the Jenkins Pipeline is configured from SCM, because Jenkins already knows the repository configuration.
🚀 Jenkins Pipeline with Docker Registry
A simplified example using Jenkins credentials:
pipeline {

    agent any

    environment {
        IMAGE_NAME = 'USERNAME/myapp'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} ."
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_TOKEN'
                    )
                ]) {
                    sh '''
                        set +x
                        echo "$DOCKER_TOKEN" | docker login \
                          --username "$DOCKER_USER" \
                          --password-stdin

                        docker push "$IMAGE_NAME:$BUILD_NUMBER"

                        docker logout
                    '''
                }
            }
        }
    }
}
This example assumes:
Jenkins Credentials ID:
dockerhub-credentials
and that the Jenkins agent has permission to execute Docker commands.
