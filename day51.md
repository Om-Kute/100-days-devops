🐳 Day 51 – Docker Fundamentals & Architecture
🎯 Objective

Start the Docker phase of the 100 Days of DevOps journey and understand Docker fundamentals, architecture, components, containers, images, Docker Engine, Docker Hub, and the basic container workflow.

🐳 What is Docker?

Docker is a platform for building, packaging, and running applications using containers.

A container packages an application together with the dependencies required to run it.
Key Benefits
Lightweight
Portable
Consistent environments
Fast deployment
Process isolation
Efficient resource usage
Easy scaling
📦 Containers vs Virtual Machines
Feature	Container	Virtual Machine
OS	Shares host kernel	Includes guest OS
Size	Usually smaller	Usually larger
Startup	Very fast	Generally slower
Resource Usage	Lower	Higher
Isolation	Process-level	Full OS-level
Common Use	Microservices, DevOps	Full OS workloads
Simple Concept
Virtual Machine

Hardware
   ↓
Hypervisor
   ↓
Guest OS
   ↓
Application
Container

Hardware
   ↓
Host OS
   ↓
Docker Engine
   ↓
Container
   ↓
Application
🏗️ Docker Architecture

Docker uses a client-server architecture.

Docker Client
      │
      ▼
Docker Daemon
      │
      ▼
Docker Engine
      │
 ┌────┼──────────────┐
 ▼    ▼              ▼
Images Containers  Networks
          │
          ▼
       Volumes

Docker can also interact with container registries such as Docker Hub.

🔧 Docker Components
1. Docker Client

The Docker CLI is used to communicate with Docker.

Example:

docker ps
docker images
docker run nginx
2. Docker Daemon

The Docker daemon is the background service that manages Docker resources.

It manages objects such as:

Images
Containers
Networks
Volumes
3. Docker Engine

Docker Engine provides the core functionality required to build and run containers.

It includes components such as:

Docker CLI
Docker daemon
REST API
Container runtime
4. Docker Images

An image is a read-only template used to create containers.

Example:

nginx image
     ↓
Container 1
Container 2
Container 3
5. Docker Containers

A container is a running or stopped instance created from an image.

Docker Image
     ↓
Docker Container
6. Docker Registry

A registry stores and distributes Docker images.

Examples:

Docker Hub
Amazon ECR
GitHub Container Registry
☁️ Docker Hub

Docker Hub is a cloud-based container registry.

It can be used to:

Store images
Download images
Share images
Maintain repositories
Collaborate with teams

Basic workflow:

Local Machine
     │
     ▼
Build Image
     │
     ▼
Docker Hub
     │
     ▼
Other Machine
     │
     ▼
Pull Image
🧩 Docker Objects

Important Docker objects include:

Object	Purpose
Image	Template for containers
Container	Running instance of an image
Volume	Persistent data storage
Network	Container communication
Dockerfile	Instructions for building images
Compose	Defines multi-container applications
🔄 Docker Workflow

The basic Docker workflow is:

Application Code
      ↓
Dockerfile
      ↓
Docker Build
      ↓
Docker Image
      ↓
Docker Run
      ↓
Docker Container
      ↓
Docker Registry
💻 Basic Docker Commands

Check Docker version:

docker --version

Get detailed Docker information:

docker info

Download an image:

docker pull nginx

List images:

docker images

Run a container:

docker run nginx

Run a container in detached mode:

docker run -d nginx

List running containers:

docker ps

List all containers:

docker ps -a

Stop a container:

docker stop <container_id>

Remove a container:

docker rm <container_id>

Remove an image:

docker rmi <image>
