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
