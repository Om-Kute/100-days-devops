🚀 Day 79/100 – Jenkins Security & Credentials
📌 Overview
On Day 79 of my 100 Days of DevOps journey, I focused on Jenkins Security and Credentials Management.
Jenkins is commonly used to automate CI/CD workflows, but because it can access source-code repositories, Docker registries, cloud platforms, and Kubernetes clusters, securing Jenkins is extremely important.
The goal of this day was to understand how to:
🔐 Secure Jenkins access
👤 Manage users and permissions
🛡️ Understand authentication and authorization
🎭 Implement Role-Based Access Control (RBAC)
🔑 Store credentials securely
🔒 Protect secrets inside pipelines
🚫 Avoid hardcoding passwords and tokens
🔗 Secure Jenkins integrations with GitHub, Docker, AWS, and Kubernetes
📋 Follow least-privilege security principles
🔐 Why Jenkins Security Matters
Jenkins pipelines often have access to sensitive resources such as:
GitHub Repository
      ↓
    Jenkins
      ↓
Docker Registry
      ↓
    AWS
      ↓
 Kubernetes Cluster
If Jenkins is compromised, an attacker could potentially:
Access source code
Steal credentials
Modify builds
Push malicious Docker images
Deploy unauthorized applications
Access cloud resources
Modify Kubernetes workloads
Therefore, Jenkins should always be treated as a critical infrastructure component.
🔑 Authentication vs Authorization
Authentication
Authorization
Verifies identity
Determines permissions
"Who are you?"
"What can you do?"
Login/password/token
Roles and permissions
Happens first
Happens after authentication
Example
User
 ↓
Authentication
 ↓
Identity Verified
 ↓
Authorization
 ↓
Check Permissions
 ↓
Access Jenkins Resources
👤 Jenkins Authentication
Jenkins can authenticate users through different mechanisms.
Common options include:
Jenkins internal user database
LDAP
Active Directory
OAuth
SAML
OpenID Connect
For smaller environments, Jenkins' built-in user database may be sufficient.
For enterprise environments, centralized identity management is commonly preferred.
🛡️ Jenkins Authorization
Authorization controls what authenticated users are allowed to do.
Examples include:
Overall Jenkins administration
Job creation
Job configuration
Job execution
View access
Credential management
Agent management
Workspace access
A user should receive only the permissions required for their role.
🎭 Role-Based Access Control (RBAC)
RBAC assigns permissions based on roles rather than individually configuring every user.
Example
Jenkins
                       │
          ┌────────────┼────────────┐
          ↓            ↓            ↓
       Admin       Developer      Viewer
          │            │            │
       Full Access   Build/View    View Only
Example Roles
Role
Example Permissions
Admin
Full Jenkins administration
Developer
Build and view jobs
DevOps Engineer
Pipeline and deployment operations
Viewer
View jobs and build results
RBAC helps organizations maintain consistent and manageable permissions.
🔑 Jenkins Credentials
Jenkins provides a Credentials system for securely storing authentication information.
Instead of writing secrets directly inside a Jenkinsfile:
password = "MyPassword123"
Store the secret in Jenkins Credentials and reference it through a credential ID.
📦 Common Credential Types
Jenkins can store different types of credentials.
1. Username + Password
Used for:
Private repositories
Internal applications
Registry authentication
Example ID:
github-credentials
2. SSH Username with Private Key
Commonly used for:
Git SSH authentication
Linux servers
Remote deployment
Example:
Username: ubuntu
Private Key: ********
3. Secret Text
Useful for:
API tokens
Access tokens
Application secrets
Example:
github-token
4. Secret File
Useful for:
Configuration files
Certificates
Kubernetes kubeconfig files
Other sensitive files
5. Certificate
Can be used when authentication requires certificates.
🏗️ Adding Credentials in Jenkins
Typical process:
Jenkins Dashboard
      ↓
Manage Jenkins
      ↓
Credentials
      ↓
Choose Credential Store
      ↓
Global Credentials
      ↓
Add Credentials
      ↓
Select Credential Type
      ↓
Enter Secret
      ↓
Save
Example:
ID: github-credentials
Username: <username>
Password/Token: <token>
The exact UI can vary depending on the Jenkins version and installed plugins.
🔒 Using Credentials in Jenkinsfile
Credentials should be referenced by their Jenkins credential ID.
Example:
pipeline {
    agent any

    stages {
        stage('Use Credentials') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'github-credentials',
                        usernameVariable: 'GIT_USER',
                        passwordVariable: 'GIT_TOKEN'
                    )
                ]) {
                    sh '''
                        echo "Using authenticated operation"
                    '''
                }
            }
        }
    }
}
The secret itself should not be written into the Jenkinsfile.
🐳 Docker Credentials
Jenkins can securely authenticate with a Docker registry.
Example:
withCredentials([
    usernamePassword(
        credentialsId: 'dockerhub-credentials',
        usernameVariable: 'DOCKER_USER',
        passwordVariable: 'DOCKER_PASSWORD'
    )
]) {
    sh '''
        echo "$DOCKER_PASSWORD" | docker login \
        -u "$DOCKER_USER" \
        --password-stdin

        docker push USERNAME/my-app:$BUILD_NUMBER
    '''
}
Important
Avoid:
docker login -u username -p password
Prefer:
echo "$DOCKER_PASSWORD" | docker login \
-u "$DOCKER_USER" \
--password-stdin
This reduces the chance of exposing passwords through command history or process arguments.
