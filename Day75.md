🚀 Day 75 – Jenkins Pipeline & Jenkinsfile
🎯 Objective
Learn how to create a Jenkins Pipeline and define CI/CD automation using a Jenkinsfile, following the Pipeline-as-Code approach.
🤖 What is Jenkins Pipeline?
A Jenkins Pipeline is a suite of plugins that supports implementing and integrating continuous delivery pipelines into Jenkins.
Instead of configuring every build step through the Jenkins UI, the pipeline can be defined as code.
Git Repository
      │
      ▼
Jenkinsfile
      │
      ▼
Jenkins Pipeline
      │
      ├── Checkout
      ├── Build
      ├── Test
      └── Deploy
💻 What is a Jenkinsfile?
A Jenkinsfile is a text file that defines a Jenkins Pipeline.
It can be stored inside the application's Git repository.
Example:
my-project/
│
├── src/
├── pom.xml
├── Dockerfile
└── Jenkinsfile
This approach is called:
Pipeline as Code
 Freestyle vs Pipeline

Feature

Freestyle

Pipeline

Configuration

Jenkins UI

Code

Version Control

Limited

Jenkinsfile can be stored in Git

Complex Workflows

Limited

Excellent

Maintainability

Can become difficult

Better

Stages

Limited

Built-in pipeline stages

Parallel Execution

Limited

Supported

Code Review

Difficult

Jenkinsfile can be reviewed

Production CI/CD

Less suitable for complex workflows

Commonly preferred
🏗️ Jenkins Pipeline Architecture
GitHub
                    │
                    ▼
               Jenkinsfile
                    │
                    ▼
            Jenkins Controller
                    │
                    ▼
                  Agent
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
       Checkout   Build      Test
                              │
                              ▼
                           Deploy
📋 Declarative Pipeline
Jenkins supports different Pipeline approaches.
A Declarative Pipeline provides a structured syntax for defining CI/CD workflows.
Basic structure:
pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building application'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application'
            }
        }
    }
}
🧩 Jenkinsfile Components
A typical Declarative Pipeline contains:
pipeline
   │
   ├── agent
   │
   ├── stages
   │      │
   │      ├── stage
   │      │     └── steps
   │      │
   │      ├── stage
   │      │     └── steps
   │      │
   │      └── stage
   │            └── steps
   │
   └── post
⚙️ pipeline
The pipeline block defines the entire Jenkins Pipeline.
pipeline {
    // Pipeline configuration
}
🖥️ agent
The agent specifies where the Pipeline or a stage should execute.
Example:
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Running build'
            }
        }
    }
}
agent any allows Jenkins to select an available suitable agent.
🏗️ stages
The stages block contains the major phases of the Pipeline.
Example:
stages {

    stage('Build') {
        steps {
            echo 'Build application'
        }
    }

    stage('Test') {
        steps {
            echo 'Run tests'
        }
    }
}
📌 stage
A stage represents a logical phase of the CI/CD process.
Common stages:
Checkout
   ↓
Build
   ↓
Test
   ↓
Package
   ↓
Deploy
Example:
stage('Build') {
    steps {
        echo 'Building application'
    }
}
▶️ steps
The steps block contains the commands that Jenkins executes.
Example:
steps {
    echo 'Hello Jenkins'
}
Shell command:
steps {
    sh 'mvn clean package'
}
