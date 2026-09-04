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
🔑 Step 3 – Add Jenkins Repository
Import the Jenkins signing key:
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
Add the Jenkins repository:
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/" | \
sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
Always verify the current installation instructions from the official Jenkins documentation before installing in production because repository URLs and supported Java versions can change.
📦 Step 4 – Install Jenkins
Update package information:
sudo apt update
Install Jenkins:
sudo apt install -y jenkins
Check installation:
jenkins --version
▶️ Step 5 – Start Jenkins
Start the Jenkins service:
sudo systemctl start jenkins
Check status:
sudo systemctl status jenkins
Expected state:
Active: active (running)
🔄 Step 6 – Enable Jenkins at Boot
Enable Jenkins to start automatically after system reboot:
sudo systemctl enable jenkins
Verify:
sudo systemctl is-enabled jenkins
Expected:
enabled
🛑 Jenkins Service Commands
Start:
sudo systemctl start jenkins
Stop:
sudo systemctl stop jenkins
Restart:
sudo systemctl restart jenkins
Check status:
sudo systemctl status jenkins
Enable at boot:
sudo systemctl enable jenkins
Disable at boot:
sudo systemctl disable jenkins
🌐 Step 7 – Access Jenkins
By default, Jenkins listens on port:
8080
On the same machine:
http://localhost:8080
For a remote Ubuntu/AWS server:
http://SERVER-IP:8080
Example:
http://203.0.113.10:8080
Do not expose Jenkins broadly to the public internet without appropriate network controls and authentication.
🔐 Step 8 – Get Initial Administrator Password
Jenkins provides an initial administrator password during first-time setup.
On a standard Debian/Ubuntu package installation:
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Copy the displayed password.
Initial Administrator Password
             │
             ▼
       Jenkins Login
🔓 Step 9 – Unlock Jenkins
Open the Jenkins web interface:
http://SERVER-IP:8080
The first-time setup screen asks for the Administrator Password.
Paste the password obtained from:
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Then continue with the setup wizard.
🧩 Step 10 – Install Plugins
Jenkins provides plugin installation options.
For a basic CI/CD setup, useful plugins may include:
Git
Pipeline
Credentials
Docker
Kubernetes
Maven Integration
Email Extension
Install only the plugins that are actually required.
Keeping the plugin set smaller can reduce maintenance and security exposure.
👤 Step 11 – Create Administrator User
Create the first Jenkins administrator account.
Typical information:
Username
Password
Full Name
Email Address
Use a strong password and protect the account appropriately.
🖥️ Step 12 – Jenkins Dashboard
After completing the setup, Jenkins displays the Dashboard.
Typical areas include:
Jenkins Dashboard
       │
       ├── New Item
       ├── Build Queue
       ├── Build Executor Status
       ├── Build History
       ├── Manage Jenkins
       └── Credentials
⚙️ Step 13 – Manage Jenkins
The Manage Jenkins section provides access to important administration features.
Depending on your Jenkins version and installed plugins, you may find:
System configuration
Plugins
Tools
Security
Credentials
Nodes
System information
System log
🔐 Jenkins Credentials
Jenkins provides a credentials system for securely managing authentication information used by jobs and pipelines.
Examples:
Git Credentials
SSH Keys
API Tokens
Docker Registry Credentials
Cloud Credentials
Kubernetes Credentials
Avoid hardcoding credentials inside:
Jenkinsfile
Shell Scripts
Source Code
Git Repositories
📁 Jenkins Home Directory
For a typical Linux package installation:
/var/lib/jenkins
This directory is commonly used as JENKINS_HOME.
Conceptually:
JENKINS_HOME
     │
     ├── jobs/
     ├── plugins/
     ├── workspace/
     ├── users/
     ├── secrets/
     └── configuration files
Do not manually modify Jenkins internal files unless you understand the consequences.
