# 🚀 Day 57/100 – Docker Networking

## 📌 Topic

**Docker Networking**

Docker Networking allows containers to communicate with each other, communicate with the host system, and access external networks.

---

## 🌐 Why Docker Networking?

Docker networking is used to:

- Connect containers
- Allow container-to-container communication
- Expose applications to the host
- Provide network isolation
- Connect multiple services in an application
## 🌐 Why Docker Networking?

Docker networking is used to:

- Connect containers
- Allow container-to-container communication
- Expose applications to the host
- Provide network isolation
- Connect multiple services in an application
## 🔹 Docker Network Types

### 1. Bridge Network

The default Docker network.
bash
docker network ls
Containers connected to the default bridge network can communicate through the Docker bridge.

2. Host Network
The container uses the host machine's network stack.
docker run --network host nginx
There is less network isolation between the container and host.

3. None Network
The container has no network connectivity.
docker run --network none nginx
Useful when complete network isolation is required.
