# 🐳 Day 55 – Docker Volumes & Persistent Data

## 🎯 Objective

Learn how Docker manages persistent data using Volumes and Bind Mounts, and understand how data can survive beyond the lifecycle of a container.

## 💾 Why Docker Volumes?

Containers are ephemeral. Data stored only inside a container can be lost when that container is removed.

Docker Volumes provide persistent storage independent of the container lifecycle.

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
Mount a Volume
docker run -d \
  --name mycontainer \
  -v myvolume:/data \
  nginx

The volume is mounted at:

/data

inside the container.

🧪 Practical Example

Create a volume:

docker volume create data-volume

Run a container:

docker run -it \
  --name ubuntu-container \
  -v data-volume:/data \
  ubuntu

Create persistent data:

echo "Docker Persistent Data" > /data/test.txt

Exit:

exit

Remove the container:

docker rm ubuntu-container

Create another container using the same volume:

docker run -it \
  --name ubuntu-container-2 \
  -v data-volume:/data \
  ubuntu

Check the data:

cat /data/test.txt

The data remains available because it is stored in the Docker Volume.
🔗 Bind Mount

Example:

docker run -d \
  --name web \
  -v /home/user/app:/usr/share/nginx/html \
  nginx

Bind mounts map a host directory directly into a container and are especially useful during development.

⚖️ Volume vs Bind Mount
Feature	Docker Volume	Bind Mount
Managed by Docker	✅	❌
Host path required	❌	✅
Persistent	✅	✅
Development	Good	Excellent
Database Storage	Common	Possible
🗑️ Remove Volume
docker volume rm myvolume

Remove unused volumes:

docker volume prune

⚠️ Review carefully before deleting unused volumes.

💾 Backup Concept

Volumes can be backed up by mounting them into a temporary container and creating an archive.

docker run --rm \
  -v myvolume:/data \
  -v $(pwd):/backup \
  ubuntu \
  tar czf /backup/myvolume-backup.tar.gz -C /data .
