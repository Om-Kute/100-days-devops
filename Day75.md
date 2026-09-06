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
📦 Basic Jenkinsfile
pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code'
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

        stage('Deploy') {
            steps {
                echo 'Deploying application'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed'
        }
    }
}
🔗 Git Checkout
A Jenkins Pipeline can retrieve source code from Git.
Example:
stage('Checkout') {
    steps {
        git 'https://github.com/USERNAME/REPOSITORY.git'
    }
}
For private repositories, use Jenkins-managed credentials rather than embedding credentials in the Jenkinsfile.
☕ Maven Pipeline Example
For a Java/Maven project:
pipeline {

    agent any

    stages {

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
    }
}
🧪 Test Stage
Automated testing can be included in the Pipeline.
Example:
stage('Test') {
    steps {
        sh 'mvn test'
    }
}
If the command returns a failure status, Jenkins normally marks the stage/build as failed unless the pipeline explicitly handles the error.
🚀 Deploy Stage
A deployment step can be added after successful build and test stages.
Example:
stage('Deploy') {
    steps {
        echo 'Deploying application...'
    }
}
Later this can be replaced with commands for:
Docker
Kubernetes
AWS
Cloud platforms
Application servers
📜 post Block
The post section allows actions to run after Pipeline execution.
Example:
post {

    always {
        echo 'Pipeline finished'
    }

    success {
        echo 'Pipeline successful'
    }

    failure {
        echo 'Pipeline failed'
    }
}
Common conditions include:
always
success
failure
unstable
aborted
changed
🔄 Pipeline Execution Flow
Jenkinsfile
     │
     ▼
Pipeline Start
     │
     ▼
Checkout
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
Post Actions
🖥️ Create a Pipeline Job
From the Jenkins Dashboard:
New Item
   ↓
Enter Name
   ↓
Pipeline
   ↓
OK
Example:
my-first-pipeline
⚙️ Configure Pipeline
Inside the Pipeline configuration:
Pipeline
   │
   ├── Definition
   │
   ├── Pipeline script
   │
   └── Pipeline script from SCM
For a learning test, you can use:
Pipeline script
For a real project, prefer storing the Jenkinsfile in source control:
Pipeline script from SCM
📁 Jenkinsfile from Git
Recommended project structure:
GitHub Repository
       │
       ├── src/
       ├── pom.xml
       ├── Dockerfile
       └── Jenkinsfile
Jenkins retrieves the Jenkinsfile from the repository.
GitHub
   │
   ▼
Jenkins
   │
   ▼
Read Jenkinsfile
   │
   ▼
Execute Pipelineu
🟢 Run Pipeline
After saving the Pipeline:
Build Now
Jenkins executes:
Checkout
   ↓
Build
   ↓
Test
   ↓
Deploy
📊 Stage View
Jenkins provides stage-level visibility.
Example:
Build #1

Checkout    Build    Test    Deploy
   ✅         ✅       ✅       ✅
If a stage fails:
Checkout    Build    Test    Deploy
   ✅         ✅       ❌       ⏸️
This makes troubleshooting easier.
📜 Console Output
Open the build and select:
Console Output
Example:
Started by user

[Pipeline] Start
[Pipeline] stage
[Pipeline] { (Build)

Building application...

[Pipeline] }
[Pipeline] stage
[Pipeline] { (Test)

Running tests...

[Pipeline] }
[Pipeline] stage
[Pipeline] { (Deploy)

Deploying application...

[Pipeline] }

Finished: SUCCESS
