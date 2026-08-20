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
