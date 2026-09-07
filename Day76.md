🚀 Day 76 – Jenkins + GitHub Integration
🎯 Objective
Learn how to integrate Jenkins with GitHub and automatically trigger Jenkins CI/CD pipelines whenever new code is pushed to a GitHub repository.
🔗 Jenkins + GitHub
Jenkins can integrate with GitHub to automatically start CI/CD jobs when developers push code.
Basic workflow:
Developer
    │
    │ git push
    ▼
 GitHub Repository
    │
    │ Webhook
    ▼
   Jenkins
    │
    ▼
 Jenkins Pipeline
    │
    ├── Checkout
    ├── Build
    ├── Test
    └── Deploy
🚀 Why Integrate Jenkins with GitHub?
Without automation:
Developer
    ↓
Push Code
    ↓
Open Jenkins
    ↓
Click Build Now
With GitHub Webhooks:
Developer
    ↓
Push Code
    ↓
GitHub
    ↓
Webhook
    ↓
Jenkins
    ↓
Automatic Build 🚀
This creates a faster and more automated CI/CD feedback loop.
🔔 What is a GitHub Webhook?
A GitHub Webhook allows GitHub to send an HTTP request to an external service when specific repository events occur.
For example:
git push
   ↓
GitHub Event
   ↓
Webhook
   ↓
Jenkins
   ↓
Pipeline Trigger
Common events include:
Push
Pull request
Release
Tag
Branch-related events
For a basic Jenkins CI workflow, the push event is commonly used.
🏗️ Complete Architecture
Developer
                        │
                     git push
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
                  Jenkins Pipeline
                        │
              ┌─────────┼─────────┐
              ▼         ▼         ▼
           Checkout    Build     Test
                                  │
                                  ▼
                               Deploy
                                  │
                                  ▼
🧩 Jenkins Plugins
Depending on the Jenkins setup, plugins commonly used for GitHub integration include:
Git Plugin
GitHub Plugin
Pipeline Plugin
Credentials Plugin
GitHub Branch Source Plugin
Install only the plugins required for your workflow.
Go to:
Manage Jenkins
      ↓
Plugins
Search for the required integrations.                             Application
