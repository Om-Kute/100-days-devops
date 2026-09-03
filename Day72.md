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
📋 Jenkins Jobs
A Job defines work that Jenkins should perform.
Example:
Job
 │
 ├── Checkout Code
 ├── Build
 ├── Test
 ├── Package
 └── Deploy
Common Jenkins job types include:
Freestyle Project
Pipeline
Multibranch Pipeline
Organization Folder
🔨 Jenkins Build
A Build is an execution of a Jenkins job.
Example:
Job
 │
 ├── Build #1 → SUCCESS
 ├── Build #2 → SUCCESS
 ├── Build #3 → FAILURE
 └── Build #4 → SUCCESS
Every build gets a build number.
Example:
Build #42
⚙️ Executors
An Executor is a slot that allows a Jenkins node to run a build.
Example:
Agent
 │
 ├── Executor 1 → Build A
 ├── Executor 2 → Build B
 └── Executor 3 → Build C
More executors can allow more parallel work, but actual concurrency depends on available CPU, memory, I/O, and other resources.
📁 Jenkins Workspace
A workspace is a directory where Jenkins performs a job's work.
Typical workflow:
Workspace
    │
    ├── Clone Repository
    ├── Compile Code
    ├── Run Tests
    └── Create Artifacts
A Pipeline may use a workspace on the node/agent where its steps execute.
🧩 Jenkins Plugins
Plugins extend Jenkins functionality.
Examples include integrations for:
Git
GitHub
Maven
Docker
Kubernetes
Slack
Email
Cloud Platforms
The plugin ecosystem allows Jenkins to integrate with many DevOps tools.
🔗 Jenkins Ecosystem
A typical Jenkins environment can look like:
                   Jenkins
                      │
       ┌──────────────┼──────────────┐
       ▼              ▼              ▼
      Git           Docker       Kubernetes
       │              │              │
       ▼              ▼              ▼
   Source Code    Container       Deployment
🔄 Jenkins CI/CD Workflow
A common Jenkins workflow:
Developer
    │
    ▼
GitHub
    │
    ▼
Webhook / Trigger
    │
    ▼
Jenkins Controller
    │
    ▼
Agent
    │
    ├── Checkout
    ├── Build
    ├── Test
    ├── Package
    └── Deploy
    │
    ▼
Application
🔥 Example Workflow
Suppose we have a Java application.
Step 1 – Developer Push
git add .
git commit -m "Update application"
git push
Step 2 – Jenkins Trigger
GitHub can notify Jenkins using a webhook.
GitHub
   │
   ▼
Webhook
   │
   ▼
Jenkins
Step 3 – Build
mvn clean package
Step 4 – Test
mvn test
Step 5 – Docker Build
docker build -t myapp:1.0 .
Step 6 – Deployment
The image can then be deployed to a suitable environment such as Kubernetes.
Jenkins
   │
   ▼
Docker Image
   │
   ▼
Kubernetes
🏗️ Detailed Jenkins Architecture
                         Users
                           │
                           ▼
                  Jenkins Controller
                           │
       ┌───────────────────┼───────────────────┐
       │                   │                   │
       ▼                   ▼                   ▼
  Job Management     Build Scheduling    Plugin Management
       │                   │                   │
       └───────────────────┼───────────────────┘
                           │
                           ▼
                      Jenkins Agents
                    ┌──────┼──────┐
                    ▼      ▼      ▼
                  Agent1 Agent2 Agent3
                    │      │      │
                    ▼      ▼      ▼
                  Build  Test   Deploy
