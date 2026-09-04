🚀 Day 73 – Jenkins Installation & Setup
🎯 Objective
Install and configure Jenkins on Ubuntu and prepare a working Jenkins server for CI/CD automation.
🤖 What is Jenkins?
Jenkins is an open-source automation server used to automate software development processes such as:
Code
  ↓
Build
  ↓
Test
  ↓
Package
  ↓
Deploy
Jenkins can integrate with tools such as:
Git
GitHub
Maven
Docker
Kubernetes
AWS
Slack
Email
🏗️ Jenkins Installation Architecture
Ubuntu Server
                       │
                       ▼
                    Java/JDK
                       │
                       ▼
                    Jenkins
                       │
              ┌────────┴────────┐
              ▼                 ▼
         Jenkins UI         Jenkins Service
              │                 │
              ▼                 ▼
          Port 8080          systemd
              │
              ▼
          CI/CD Jobs
