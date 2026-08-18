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
🔗 Docker Network Drivers

Docker provides different network drivers for different use cases.

Network	Purpose
Bridge	Default network for containers on a Docker host
Host	Container shares host networking
None	Disables container networking
Overlay	Multi-host container communication
Macvlan	Gives containers network identities on the physical network
1️⃣ Bridge Network
The bridge network is the default network driver for containers.

Docker Host
     │
     ▼
  Bridge
  /    \
 ↓      ↓
Web    DB

Containers connected to the same user-defined bridge network can communicate with each other.
2️⃣ Host Network
With the host network:
docker run --network host nginx
The container shares the host's network namespace.
There is no separate container network isolation in the usual bridge-network sense.
3️⃣ None Network
The none network disables networking for the container.
docker run --network none nginx
This can be useful when a workload should have no network connectivity.
4️⃣ Overlay Network
Overlay networks allow communication between containers running across multiple Docker hosts.

They are commonly associated with Docker Swarm.

Host 1                 Host 2
   │                      │
Container              Container
   │                      │
   └──── Overlay Network ──┘
