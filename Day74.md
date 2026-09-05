🚀 Day 74 – Jenkins Freestyle Jobs & Build Triggers
🎯 Objective
Learn how to create and configure a Jenkins Freestyle Project, connect it with Git/GitHub, add build steps, execute jobs, analyze build results, and understand different Jenkins build triggers.
🤖 What is a Jenkins Freestyle Project?
A Freestyle Project is a traditional Jenkins job type that allows you to configure build and automation tasks through the Jenkins web interface.
It is useful for learning Jenkins fundamentals and for relatively simple automation workflows.
Freestyle Project
       │
       ├── Source Code
       ├── Build Steps
       ├── Build Triggers
       ├── Post-Build Actions
       └── Build History
🏗️ Freestyle Job Architecture
Developer
    │
    ▼
GitHub Repository
    │
    ▼
Jenkins Trigger
    │
    ▼
Freestyle Job
    │
    ├── Checkout Code
    ├── Build
    ├── Test
    └── Package
    │
    ▼
Build Result
    │
    ├── SUCCESS
    └── FAILURE
🚀 Step 1 – Create a Freestyle Project
Open Jenkins Dashboard.
Select:
New Item
   ↓
Enter an item name
   ↓
Freestyle project
   ↓
OK
Example job name:
my-first-freestyle-job
⚙️ Step 2 – Configure Source Code Management
Inside the job configuration:
Source Code Management
        ↓
       Git
Enter the repository URL:
https://github.com/USERNAME/REPOSITORY.git
Example:
https://github.com/omkute/my-app.git
Configure credentials if the repository is private.
🌿 Configure Branch
Specify the branch Jenkins should build.
Example:
*/main
For another branch:
*/develop
The exact branch specification depends on the repository and SCM configuration.
📥 Jenkins Git Checkout
When the job runs:
Jenkins
   │
   ▼
Git Repository
   │
   ▼
Clone / Fetch
   │
   ▼
Workspace
Jenkins checks out the required source code into the workspace used by the build.
📁 Jenkins Workspace
The workspace is the directory where Jenkins performs the job's operations.
Conceptually:
Workspace
    │
    ├── Source Code
    ├── Dependencies
    ├── Build Files
    └── Generated Artifacts
For a typical Linux Jenkins installation, job workspaces are commonly located under:
/var/lib/jenkins/workspace/
The actual workspace location can vary depending on the node and Jenkins configuration.
🛠️ Step 3 – Add Build Steps
In the job configuration:
Build Steps
    ↓
Add build step
Common options include:
Execute Shell
Invoke top-level Maven targets
Execute Windows batch command
The available options depend on the installed Jenkins plugins and operating system.
🐧 Execute Shell
For a Linux agent, you can use:
echo "Starting Jenkins Build"

pwd

ls -la

echo "Build completed"
Jenkins executes these commands on the node where the job is running.
☕ Maven Build
For a Maven-based Java application, a build step can run:
mvn clean package
Example workflow:
Git Checkout
     ↓
Maven Build
     ↓
Unit Tests
     ↓
Package
     ↓
JAR
🧪 Example Shell Build
echo "===== Build Started ====="

echo "Current Directory:"
pwd

echo "Files:"
ls -la

echo "Running Maven Build..."

mvn clean package

echo "===== Build Completed ====="
🔨 Step 4 – Build the Job
After saving the configuration:
Jenkins Job
     ↓
Build Now
Click Build Now to manually trigger the job.
Build Now
    ↓
Build #1
    ↓
Build #2
    ↓
Build #3
Each execution receives a build number.
📊 Build History
Jenkins maintains a history of job executions.
Example:
Build #5 → SUCCESS
Build #4 → SUCCESS
Build #3 → FAILURE
Build #2 → SUCCESS
Build #1 → SUCCESS
Build history helps track:
Successful builds
Failed builds
Build duration
Console logs
Changes
Artifacts
📜 Console Output
The Console Output shows what happened during the build.
Example:
Started by user
Building in workspace /var/lib/jenkins/workspace/my-first-job

> git fetch
> git checkout main

Running build...

[INFO] Building application
[INFO] Running tests
[INFO] BUILD SUCCESS

Finished: SUCCESS
If something fails, the console output is usually the first place to investigate.
🟢 Successful Build
A successful Jenkins build normally ends with:
Finished: SUCCESS
Concept:
Code
 ↓
Build
 ↓
Test
 ↓
SUCCESS ✅
🔴 Failed Build
A failed build may look like:
Finished: FAILURE
Possible causes:
Compilation Error
Test Failure
Dependency Problem
Git Error
Shell Command Error
Environment Problem
Permission Error
Always inspect the Console Output to identify the actual failure.
⏰ Build Triggers
Jenkins provides different ways to start jobs.
Common triggers include:
Manual Trigger
      │
Poll SCM
      │
Scheduled Build
      │
Webhook
      │
Upstream Job
👆 1. Manual Trigger
The simplest method is:
Build Now
A developer or Jenkins administrator manually starts the job.
Useful for:
Testing configuration
Debugging
Manual deployments
Initial job testing
🔍 2. Poll SCM
With Poll SCM, Jenkins periodically checks the source-control repository for changes.
Concept:
Jenkins
   │
   ▼
Check Repository
   │
   ├── No Change → Do Nothing
   │
   └── Change → Start Build
Example schedule:
H/5 * * * *
This represents polling roughly every five minutes with Jenkins' hashed scheduling behavior.
Polling is different from a webhook because Jenkins periodically checks the repository instead of being directly notified of a change.
🔗 3. GitHub Webhook
A webhook allows GitHub to notify Jenkins when an event occurs.
Concept:
Developer
    │
    ▼
Git Push
    │
    ▼
GitHub
    │
 Webhook
    │
    ▼
Jenkins
    │
    ▼
Build
This can provide faster feedback than periodic polling.
🏗️ Complete Freestyle Workflow
Developer
    │
    ▼
GitHub
    │
    ▼
Webhook / Poll SCM / Manual
    │
    ▼
Jenkins Freestyle Job
    │
    ▼
Checkout Source Code
    │
    ▼
Build Step
    │
    ▼
Automated Tests
    │
    ▼
Package
    │
    ▼
Console Output
    │
    ▼
Build Result
