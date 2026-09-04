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
📋 Prerequisites
Before installing Jenkins, make sure you have:
Ubuntu server
Sudo/root privileges
Java installed
Internet connectivity
Sufficient CPU and memory
Port 8080 accessible if Jenkins needs to be reached remotely
For an AWS EC2 deployment, make sure the instance's security rules allow access to port 8080 only from trusted sources.
☕ Step 1 – Update Ubuntu
sudo apt update
Upgrade packages if required:
sudo apt upgrade -y
☕ Step 2 – Install Java
Jenkins requires a supported Java runtime.
For example:
sudo apt install -y fontconfig openjdk-21-jre
Verify:
java -version
Example:
openjdk version "21..."
Use a Java version supported by the Jenkins release you install.
