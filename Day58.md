🐳 Day 58 – Docker Compose
🎯 Objective
Learn how to define and run multi-container applications using Docker Compose and manage services, networks, volumes, ports, and environment variables from a single configuration file.
🐳 What is Docker Compose?
Docker Compose is a tool for defining and running multi-container Docker applications using a YAML configuration file.
Instead of running many Docker commands individually, we can define the complete application stack in:
compose.yaml
Example architecture:
                    Docker Compose
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
       Frontend        Backend       Database
       Container       Container      Container
          │              │              │
          └──────────────┼──────────────┘
                         ▼
                  Docker Network
📄 Compose File
A typical Compose file is named:
compose.yaml
Example:
services:

  web:
    image: nginx:alpine
    ports:
      - "8080:80"

  app:
    image: node:18-alpine
    working_dir: /app
    command: node server.js
    ports:
      - "3000:3000"

  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: example
      MYSQL_DATABASE: appdb
🧩 Main Docker Compose Components
compose.yaml
     │
     ├── Services
     │
     ├── Networks
     │
     ├── Volumes
     │
     ├── Environment Variables
     │
     └── Configuration
🔧 Services
A service represents a container configuration.
Example:
services:

  web:
    image: nginx:alpine

  app:
    image: node:18-alpine

  db:
    image: mysql:8
This defines three services:
web
app
db
🚀 Start Application
Start all services:
docker compose up
Run in background:
docker compose up -d
Docker Compose will create the required networks and containers and start the services.
📋 Check Services
docker compose ps
Example:
NAME       SERVICE    STATUS
web        web        running
app        app        running
db         db         running
📜 View Logs
View logs:
docker compose logs
Follow logs:
docker compose logs -f
View logs for a specific service:
docker compose logs app
🛑 Stop Application
docker compose stop
This stops the services without removing the containers.
🧹 Remove Application
docker compose down
This normally stops and removes the Compose-managed containers and networks.
