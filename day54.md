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
📥 Pull Image

On another system:

docker pull username/myapp:1.0

Run it:

docker run -d username/myapp:1.0
🧱 Docker Image Layers

Docker images are composed of layers.

Example:

CMD
 ↓
COPY
 ↓
RUN
 ↓
WORKDIR
 ↓
FROM

Docker can reuse cached layers during builds, which can make subsequent builds faster.
📦 Image Optimization

Important techniques:

Use appropriate lightweight base images.
Use .dockerignore.
Remove unnecessary files and packages.
Take advantage of Docker build cache.
Use multi-stage builds.
Avoid storing secrets in images.
Keep production images minimal.
🚫 .dockerignore

Example:

node_modules
.git
.gitignore
*.log
.env
README.md

This prevents unnecessary files from being sent as part of the Docker build context.

🏗️ Multi-Stage Build

Example:

FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

FROM node:18-alpine

WORKDIR /app

COPY --from=builder /app/dist ./dist

EXPOSE 3000

CMD ["node", "dist/app.js"]
Benefits
Smaller final image
Fewer unnecessary dependencies
Cleaner production image
Reduced attack surface
