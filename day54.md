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
