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
