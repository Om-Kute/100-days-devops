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

Docker can also interact with contain
