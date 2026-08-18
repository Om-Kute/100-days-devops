# 🌐 Day 56 – Docker Networking

## 🎯 Objective

Learn how Docker networking enables containers to communicate with each other, the Docker host, and external networks.
# 🌐 What is Docker Networking?

Docker networking provides communication between:

- Containers
- Containers and the host
- Containers and external networks
- Applications running across multiple containers

Basic architecture:

text
Internet
    ↓
Host Machine
    ↓
Docker Network
    ├── Container 1
    ├── Container 2
    └── Container 3
