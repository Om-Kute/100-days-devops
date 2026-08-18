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
5️⃣ Macvlan Network

Macvlan allows containers to appear as network devices on the physical network.

This can be useful for workloads that need to integrate directly with an existing Layer 2 network.
🛠️ Important Docker Network Commands
List Networks
docker network ls
Create a Network
docker network create mynetwork
Inspect a Network
docker network inspect mynetwork
Connect Container to Network
docker network connect mynetwork container_name
Disconnect Container
docker network disconnect mynetwork container_name
Remove Network
docker network rm mynetwork
🚀 Custom Bridge Network

Create a custom network:

docker network create app-network

Run an Nginx container:

docker run -d \
  --name web \
  --network app-network \
  nginx

Run another container:

docker run -it \
  --name client \
  --network app-network \
  ubuntu

Now both containers are connected to:

app-network
🔄 Container-to-Container Communication

Containers on the same user-defined bridge network can communicate using container names.

app-network
     │
 ┌───┴────┐
 ▼        ▼
 web      client
Nginx    Ubuntu

From the client container:

curl http://web

The name web can be resolved through Docker's embedded DNS on the user-defined network.
🔀 Port Mapping

Port mapping exposes a container port through a host port.

Example:

docker run -d \
  -p 8080:80 \
  --name web \
  nginx

Architecture:

Host Port 8080
      │
      ▼
Container Port 80
      │
      ▼
    Nginx

Access:

http://localhost:8080

On a remote server:

http://SERVER-IP:8080

The server firewall or cloud Security Group must also allow the required port.
