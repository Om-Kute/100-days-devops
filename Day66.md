☸️ Day 66 – Kubernetes ConfigMaps & Secrets
🎯 Objective
Learn how Kubernetes manages application configuration and sensitive information using ConfigMaps and Secrets.
📋 Why ConfigMaps & Secrets?
Applications often need configuration values that should not be hardcoded into application source code.
Application Code
       │
       ├── Configuration
       │       ↓
       │    ConfigMap
       │
       └── Sensitive Data
               ↓
             Secret
This allows the same application image to be configured differently for development, testing, and production.
🗂️ ConfigMap
A ConfigMap stores non-sensitive configuration data.
Examples:
Application configuration
Environment variables
Feature flags
URLs
Log levels
Configuration files
Example:
apiVersion: v1
kind: ConfigMap

metadata:
  name: app-config

data:
  APP_NAME: "MyApplication"
  APP_ENV: "production"
  LOG_LEVEL: "info"
🔐 Secret
A Kubernetes Secret is intended for sensitive information.
Examples:
Passwords
API keys
Tokens
TLS certificates
Database credentials
Example:
apiVersion: v1
kind: Secret

metadata:
  name: db-secret

type: Opaque

stringData:
  DB_USER: admin
  DB_PASSWORD: mypassword
Using stringData lets Kubernetes handle the conversion into the Secret's stored representation.
⚖️ ConfigMap vs Secret
Feature
ConfigMap
Secret
Purpose
Non-sensitive configuration
Sensitive information
Typical data
URLs, settings, flags
Passwords, tokens, keys
Environment variables
✅
✅
Volume files
✅
✅
Base64 representation in manifests
Not required
Commonly used
Security requirements
Normal access control
Strong access control recommended
Important: Base64 encoding is not encryption. Anyone who can obtain the encoded value can decode it.
🏗️ How They Work
ConfigMap / Secret
        │
        ▼
       Pod
        │
        ▼
    Application
They can be consumed as:
ConfigMap / Secret
       │
       ├── Environment Variables
       │
       └── Mounted Files
🗂️ Create a ConfigMap
From Literal Values
kubectl create configmap app-config \
  --from-literal=APP_ENV=production \
  --from-literal=LOG_LEVEL=info
Check:
kubectl get configmaps
Describe:
kubectl describe configmap app-config
📄 Create ConfigMap from File
Create a configuration file:
nano app.properties
Example:
APP_NAME=MyApplication
APP_ENV=production
LOG_LEVEL=info
Create ConfigMap:
kubectl create configmap app-config \
  --from-file=app.properties
Check:
kubectl get configmap app-config
📁 Create ConfigMap from Directory
kubectl create configmap app-config \
  --from-file=./configs/
This loads configuration files from the specified directory.
🔐 Create a Secret
Create a Secret from literal values:
kubectl create secret generic db-secret \
  --from-literal=DB_USER=admin \
  --from-literal=DB_PASSWORD=mypassword
Check:
kubectl get secrets
Describe:
kubectl describe secret db-secret
Avoid putting real production credentials directly into shell history or Git-tracked files.
🌱 Use ConfigMap as Environment Variables
Example:
apiVersion: v1
kind: Pod

metadata:
  name: configmap-env-pod

spec:
  containers:
    - name: app
      image: nginx:alpine

      envFrom:
        - configMapRef:
            name: app-config
The ConfigMap values become environment variables inside the container.
🌱 Use a Specific ConfigMap Value
apiVersion: v1
kind: Pod

metadata:
  name: app-pod

spec:
  containers:
    - name: app
      image: nginx:alpine

      env:
        - name: APP_ENV
          valueFrom:
            configMapKeyRef:
              name: app-config
              key: APP_ENV
📁 Mount ConfigMap as Files
Example:
apiVersion: v1
kind: Pod

metadata:
  name: configmap-volume-pod

spec:
  containers:
    - name: app
      image: nginx:alpine

      volumeMounts:
        - name: config-volume
          mountPath: /etc/config

  volumes:
    - name: config-volume
      configMap:
        name: app-config
The ConfigMap data becomes available as files under:
/etc/config
🔑 Use Secret as Environment Variables
Example:
apiVersion: v1
kind: Pod

metadata:
  name: secret-env-pod

spec:
  containers:
    - name: app
      image: nginx:alpine

      env:
        - name: DB_USER
          valueFrom:
            secretKeyRef:
              name: db-secret
              key: DB_USER

        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: db-secret
              key: DB_PASSWORD
