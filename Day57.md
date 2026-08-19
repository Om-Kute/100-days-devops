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

4. Custom Bridge Network
A user-defined network provides better container-to-container communication.
Create a network:
docker network create my-net
Check networks:
docker network ls

🔗 Container-to-Container Communication
Create a database container:
docker run -d \
  --name db \
  --network my-net \
  mysql
Create an application container:
docker run -d \
  --name app \
  --network my-net \
  myapp
Because both containers are connected to my-net, the application can communicate with the database using:
db
Instead of using the database container's IP address.

🔀 Port Mapping
Port mapping exposes a container application to the host machine.
Example:
docker run -d \
  -p 8080:80 \
  --name web \
  nginx
Meaning
Host Port     Container Port
   8080   →       80
The Nginx application running inside the container on port 80 can be accessed through:
http://localhost:8080
🛠️ Important Docker Network Commands
List networks
docker network ls
Inspect a network
docker network inspect <network_name>
Create a network
docker network create <network_name>
Remove a network
docker network rm <network_name>
Connect a container to a network
docker network connect <network_name> <container_name>
Disconnect a container
docker network disconnect <network_name> <container_name>
Run a container on a specific network
docker run -d \
  --network <network_name> \
  --name <container_name> \
  <image>
🧪 Useful Connectivity Test
Enter a running container:
docker exec -it <container_name> bash
Then test connectivity:
ping <container_name>
