🚀 Day 72 – Jenkins Introduction & Architecture
🎯 Objective
Learn the fundamentals of Jenkins, understand its architecture and components, and see how Jenkins fits into the CI/CD workflow.
🤖 What is Jenkins?
Jenkins is an open-source automation server used to automate software development processes such as:
Building applications
Running automated tests
Packaging applications
Creating Docker images
Deploying applications
Triggering CI/CD pipelines
Simple concept:
Developer
    │
    ▼
   Git
    │
    ▼
 Jenkins
    │
    ├── Build
    ├── Test
    ├── Package
    └── Deploy
🚀 Why Jenkins?
Jenkins helps DevOps teams automate repetitive tasks.
Key Benefits
Open source
Large plugin ecosystem
Supports CI/CD
Integrates with Git and GitHub
Supports Docker
Supports Kubernetes
Supports cloud platforms
Automates builds and tests
Supports distributed builds
Highly customizable
🏗️ Jenkins Architecture
A basic Jenkins architecture looks like:
                    Jenkins
                       │
              ┌────────┴────────┐
              │                 │
         Controller          Agents
              │                 │
      ┌───────┼───────┐    ┌────┼────┐
      │       │       │    │    │    │
    Jobs   Plugins  Config  A1   A2   A3
              │
              ▼
         Build Scheduling
🧠 Jenkins Controller
The Jenkins Controller is responsible for coordinating Jenkins operations.
It can:
Manage Jenkins configuration
Manage jobs
Schedule builds
Manage plugins
Manage credentials
Assign work to agents
Provide the Jenkins web interface
Track build results
Conceptually:
Users
  │
  ▼
Jenkins Controller
  │
  ├── Manage Jobs
  ├── Schedule Builds
  ├── Manage Plugins
  ├── Manage Credentials
  └── Distribute Work
Modern Jenkins terminology generally uses Controller rather than the older "Master" terminology.
🖥️ Jenkins Agents
Agents are machines that execute Jenkins workloads.
An agent can be:
A physical machine
A virtual machine
A cloud instance
A container
A Kubernetes Pod
Architecture:
Jenkins Controller
       │
       ├──────────────┐
       ▼              ▼
   Agent 1         Agent 2
       │              │
       ▼              ▼
    Build           Test
Agents are useful when workloads need different operating systems, tools, or environments.
