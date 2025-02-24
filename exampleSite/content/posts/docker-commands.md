+++
title = "Docker Commands"
image = "/images/post/dockercommands.jpg"
author = "Sedat"
date = "2025-02-24T00:02:01Z"
description = "docker commands compose"
categories = ["Docker"]
type = "post"

+++
Docker commands are essential for managing and interacting with Docker containers and images. Key commands include docker run, which creates and starts a container from an image, and docker ps, which lists all running containers. To stop and remove containers, docker stop and docker rm are used, respectively. The docker build command is crucial for creating custom images from a Dockerfile, while docker pull downloads images from Docker Hub. For inspecting containers or images, docker inspect provides detailed information, and docker logs allows you to view logs of a running or stopped container. Additionally, docker-compose commands, such as docker-compose up and docker-compose down, are used for managing multi-container applications defined in a docker-compose.yml file. These commands are foundational for efficient Docker container management and application deployment.

##### Getting started
```
Install and Getting Started
Official Docker: https://docs.docker.com/get-docker/
Official Portainer: https://docs.portainer.io/start/install/server/docker
Quick Commands
Run a new container
New Image - docker run IMAGE
Name Container and Launch Image - docker run --name CONTAINER IMAGE
Map Container Ports and Launch Image -docker run -p HOSTPORT:CONTAINERPORT IMAGE
Map ALL Ports and Launch Image - docker run -P IMAGE
Launch Image as Background Service - docker run -d IMAGE
Map Local Directory and Launch - docker run -v HOSTDIR:TARGETDIR IMAGE
Manage Containers
List RUNNING Containers - docker ps
List ALL containers - docker ps -a
Delete container - docker rm CONTAINER
Delete a Running Container - docker rm -f CONTAINER
Stop Container - docker stop CONTAINER
Start Container - docker start CONTAINER
Copy File FROM container - docker cp CONTAINER:SOURCE TARGET
Copy File TO container - docker cp TARGET CONTAINER:SOURCE
Start Shell inside container - docker exec -it CONTAINER bash
Rename container - docker rename OLD NEW
Create new Image from Container - docker commit CONTAINER
Manage Images
Download Image - docker pull IMAGE[:TAG]
Upload Image to repository - docker push IMAGE
Delete Image - docker rmi IMAGE
List Images - docker images
Build Image from Docker file - docker build DIRECTORY
Tag Image IMAGE - docker tag IMAGE NEWIMAGE:TAG
Troubleshooting and Information
Show logs - docker logs CONTAINER
Show stats - docker stats
Show processes - docker top CONTAINER
Show modified files - docker diff CONTAINER
Show mapped ports - docker port CONTAINER
Show stoppped containers - docker ps -f "status=exited"
```
***
#####  To create the Docker network:
```
docker network create \
  --driver bridge \
  --subnet=192.168.1.0/24 \
  --gateway=192.168.1.1 \
  --opt "com.docker.network.bridge.name"="br-eth0" \
  my_custom_network

  Explanation:
--driver bridge: Specifies the network driver (bridge in this case).
--subnet=192.168.1.0/24: Defines the subnet for the network.
--gateway=192.168.1.1: Sets the gateway for the network.
--opt "com.docker.network.bridge.name"="br-eth0": Assigns the network bridge to the eth0 adapter.
my_custom_network: The name of your Docker network.

2. Assign Containers to the Network
When you run a container, use the --network flag to assign it to the new network:

docker run --rm -it --network=my_custom_network alpine sh
This will connect the container to the my_custom_network with the specified subnet.
```
***
##### Docker networking
```
list docker networks
docker network ls

docker container shell access
docker exec -it dockername /bin/sh
or
sudo docker exec -it dockername sh

lists used space images, containers, cache..
docker system df

get information about container
docker inspect nginx

get information about docker network
docker network inspect bridge

duplicate running image
docker commit hash1 test1

login to dockerhub remote server
docker login

tag docker image
docker tag my-image:latest my-repo/my-image:v1.0

push image to remote repository
docker push my-repo/my-image:v1.0

save docker image to local drive
sudo docker save -o test.tar test

load saved image from other machine
sudo docker load -i test.tar

restarts all containers
docker restart $(docker ps -q)

for windows pulling image
docker build -t phocean/beef

for linux
docker pull phocean/beef

find ip address of docker container
docker exec -it beef ifconfig eth0

list to find only id name and port of containers
docker ps --format '{{ .ID }}\t{{.Names}}\t{{ .Ports }}'

recreate container
docker-compose up -d --force-recreate
```
***
#####
```
bridge network create and container deployment

docker network create asgard

docker run -itd --rm --network asgard --name loki busybox
```
***
##### Macvlan network create and container deployment (with 802.1q)
```
docker network create -d macvlan \
--subnet 192.168.1.0/24 \
--gateway 192.168.1.1 \
-o parent=eth0 \
newasgard

sudo docker run -itd --rm --network newasgard \
--ip 192.168.1.173 \
--name thor busybox






if we tryto ping outside or our gateway we not get any answer. becouse we are trying to out from host mac address and only one ethernet mac address host uses going to router.
this reason we need to activate promiscuous

if we check mac address same with our ubuntu host machine.
PS C:\Users\sedat> arp -a 192.168.1.171

sudo ip link set eth0 promisc on

if you are using virtualbox you need to enable virtualmachine settings networking>adapter>promiscuous mode allow all





this one we made is bridge networking. and we have another mode 802.1q tunking.
router on a stick and docker works on machine and expose sub interfaces wits that method.
now lets stop containers we created and remove newasgard network

sudo docker network create -d macvlan --subnet 192.168.20.0/24 --gateway 192.168.20.1 -o parent=eth0.20 macvlan20


2 diffrent network using same interface in this example:

sedat@debian2:~$ sudo docker network create -d ipvlan \
--subnet 192.168.94.0/24 \
-o parent=eth0 -o ipvlan_mode=l3 \
--subnet 192.168.95.0/24 \
newasgard





creating container using same adapter:

sudo docker run -itd --rm --network newasgard --ip 192.168.95.7 --name thor4 busybox

sudo docker run -itd --rm --network newasgard --ip 192.168.94.7 --name thor busybox
```
***
##### Ipvlan network create and container deployment
```
sudo docker network create -d ipvlan \
--subnet 192.168.1.0/24 \
--gateway 192.168.1.1 \
-o parent=eth0 \
newasgard

sudo docker run -itd --rm --network newasgard \
--ip 192.168.1.171 \
--name thor busybox
```
***
##### How to link multiple docker-compose services via network
```
Creating the network
docker network create external-example

Modified first and second docker-compose file with network configured
version: '3'
services:
  service1:
    image: busybox
    command: sleep infinity

networks:
  default:
    external:
      name: external-example

```
***
##### Configure the default bridge network
```
To configure the default bridge network, you specify options in daemon.json. Here is an example daemon.json with several options specified. Only specify the settings you need to customize.

{
  "bip": "192.168.1.1/24",
  "fixed-cidr": "192.168.1.0/25",
  "fixed-cidr-v6": "2001:db8::/64",
  "mtu": 1500,
  "default-gateway": "192.168.1.254",
  "default-gateway-v6": "2001:db8:abcd::89",
  "dns": ["10.20.1.2","10.20.1.3"]
}
Restart Docker for the changes to take effect.
```
***
##### Disable ipv6 for docker networking
```
If you are looking to disable IPv6 from within a Linux Docker image, this seems to work even when the file system is read-only.

sysctl net.ipv6.conf.all.disable_ipv6=1
sysctl net.ipv6.conf.default.disable_ipv6=1
ifconfig | grep inet

for alpine linux:
echo net.ipv6.conf.all.disable_ipv6=1 | tee -a /etc/sysctl.conf && sysctl -p
echo net.ipv6.conf.default.disable_ipv6=1 | tee -a /etc/sysctl.conf && sysctl -p
ifconfig | grep inet
```
***
##### Cleanup script
```
Check your portainer status page and look for “unused” images and containers. If you are seeing a lot of these, then you are wasting space and I’d recommend running this script to clean them up!

The Cleanup Script
Run this bash script every week to ensure the cleanup gets performed.

#!/bin/bash

docker volume rm $(docker volume ls -f dangling=true -q)
docker rmi $(docker images --quiet --filter "dangling=true")
```
***
##### Connecting to remote docker socket or switch between them
```
docker context list

docker context create srv-demo-1 --description "Docker on srv-demo-1" --docker "host=ssh://srv-demo-1.home.clcreative.de"

docker context use srv-demo-1
```
***
