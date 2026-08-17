# 🐳 Day 55 – Docker Volumes & Persistent Data

## 🎯 Objective

Learn how Docker manages persistent data using Volumes and Bind Mounts, and understand how data can survive beyond the lifecycle of a container.

## 💾 Why Docker Volumes?

Containers are ephemeral. Data stored only inside a container can be lost when that container is removed.

Docker Volumes provide persistent storage independent of the container lifecycle.

```text
Container
    ↓
Docker Volume
    ↓
Persistent Data

Create a Volume
docker volume create myvolume

List Volumes
docker volume ls
🔍 Inspect a Volume
docker volume inspect myvolume
