# 🐳 Day 53 – Dockerfile | Build Your Own Docker Image

## 🎯 Objective

Learn how to create a custom Docker image using a Dockerfile and understand the most important Dockerfile instructions
## 📄 What is a Dockerfile?

A Dockerfile is a text file containing instructions used by Docker to automatically build a container image.

Think of it as a **recipe for creating a Docker image**.

```text
Dockerfile
     ↓
docker build
     ↓
Docker Image
     ↓
docker run
     ↓
Container
🧩 Important Dockerfile Instructions
Instruction	Purpose
FROM	Defines the base image
RUN	Executes commands during image build
COPY	Copies files from build context
ADD	Copies files and supports additional source handling
WORKDIR	Sets the working directory
ENV	Defines environment variables
EXPOSE	Documents a port used by the application
CMD	Defines the default command
ENTRYPOINT	Configures the main executable
USER	Sets the user for subsequent commands/runtime
ARG	Defines build-time variables
VOLUME	Defines a mount point
HEALTHCHECK	Defines a container health check
LABEL	Adds metadata to the image

🏗️ Dockerfile Example
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
ENV NODE_ENV=production
CMD ["node", "app.js"]
🔍 Dockerfile Explanation
FROM
FROM node:18-alpine

Defines the base image.
WORKDIR
WORKDIR /app
Sets /app as the working directory for subsequent instructions.
COPY
COPY package*.json ./
Copies package files from the build context into the image.
RUN
RUN npm install
Executes a command while building the image.
COPY Application Code
COPY . .
Copies the application source into the image.
EXPOSE
EXPOSE 3000

Documents that the application listens on port 3000.

EXPOSE does not publish the port by itself. Port publishing is done with docker run -p.

ENV
ENV NODE_ENV=production

Sets an environment variable inside the image/container environment.

CMD
CMD ["node", "app.js"]

Defines the default command executed when the container starts.
