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
