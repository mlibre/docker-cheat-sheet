# Docker

- [Installation](#installation)
- [Enabling, Disabling](#enabling-disabling)
- [Info](#info)
- [Listing](#listing)
- [Pulling](#pulling)
- [Removing](#removing)
- [Running](#running)
  - [Example](#example)
- [Log](#log)
- [Build](#build)
- [Other commands](#other-commands)
- [G tmpFs](#g-tmpfs)
- [Telegram Example](telegram/readme.md)

## Installation

```bash
sudo pacman -S docker
sudo usermod -aG docker $USER
sudo systemctl restart docker
sudo reboot
```

## Enabling, Disabling

```bash
sudo systemctl enable containerd.service
sudo systemctl enable docker.service

sudo systemctl disable containerd.service
sudo systemctl disable docker.service

sudo systemctl start containerd.service
sudo systemctl start docker.service

sudo systemctl stop containerd.service
sudo systemctl stop docker.service
```

## Info

```bash
docker info # docker info

docker COMMAND --help # command info, 
docker ps --help 
```

## Listing

```bash
# Images
docker images -a
# Containers
docker ps -a
```

## Pulling

```bash
docker pull ubuntu
docker pull ubuntu:14.04
```

## Removing

```bash
docker rmi IMAGE_NAME
docker rm CONTAINER_NAME

docker system prune -a -f # To remove any unused image, container
docker system prune --volumes -f -a # also removing volumes
```

## Running

```bash
docker run IMAGE_NAME
# check if there is a local image. if there is, will create a new container based on the local image and run it.
# if not, will try to find and download the image from the hub.docker.com
# Then will create a new container based on the downloaded image

docker start CONTAINER_NAME
# start a container

docker stop CONTAINER_NAME
# stop a container
```

### Example

```bash
docker run -d --name cname -p 80:8080 hello-world
# -d: detached, background
# --name: container name
# -p: map container port to os port
# 80: OS port
# 8080: container port
# hello-world: Image Name
docker start cname
docker logs cname

docker run -it bash
docker run -it bash /usr/local/bin/bash 
# -it: interactive mode. it will open a terminal after running the container
# /usr/local/bin/bash: the shell to open. if not specified the default path will be used
# CTRL + D or exit: to close the bash and so the container
# CTRL + P then CTRL + Q: to exit without stopping the container
```

## Log

```bash
docker logs CONTAINER_ID_OR_NAME
```

## Build

```bash
docker build --tag imageName:tag .
```

## Other commands

```bash
docker exec -ti -u root CONTAINER_NAME bash
echo "nameserver 8.8.8.8" > /etc/resolv.conf
```

## 8G tmpFs

```bash
nano /etc/fstab
tmpfs /tmp  tmpfs defaults,noatime,size=8G,mode=1777 0 0
```
