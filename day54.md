🐳 Day 54 – Building & Managing Docker Images
🎯 Objective

Learn how to build, tag, inspect, optimize, publish, and manage Docker images.
🏗️ Docker Image Workflow
Dockerfile
     ↓
docker build
     ↓
Docker Image
     ↓
Tag
     ↓
Test
     ↓
Optimize
     ↓
Push to Registry
     ↓
Deploy
🔨 Build Docker Image
docker build -t myapp:1.0 .
Explanation
docker build → Build image
-t           → Assign name and tag
myapp:1.0    → Image name + version
.            → Build context
📋 List Images
docker images
or:
docker image ls
🔍 Inspect Image
docker image inspect myapp:1.0
🏷️ Image Tagging
Tags help identify image versions.
myapp:1.0
myapp:1.1
myapp:2.0
Create a new tag:
docker tag myapp:1.0 username/myapp:1.0
🚀 Push Image to Docker Hub
Login:
docker login
Tag:
docker tag myapp:1.0 username/myapp:1.0
Push:
docker push username/myapp:1.0
This provides detailed information about the image configuration, metadata, architecture, environment, and layers.

📜 View Image History
docker history myapp:1.0

This shows the image's layer history and Dockerfile instructions that contributed to the image.
