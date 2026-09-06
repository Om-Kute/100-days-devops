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
