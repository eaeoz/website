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
##### Bridge network create and container deployment
```
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
##### Docker swarm init, depoyment and loadbalance
```
docker swarm init

docker swarm join --token SWMTKN-1-0f7vbc1it3p8ofowfh1exbbt9uxjf9c2cdh1vyx4kfbi4ky1jz-28haocvmk8pow6c0te1lh4dk5 192.168.1.243:2377
copy this line and paste on other node




docker swarm join --token SWMTKN-1-0f7vbc1it3p8ofowfh1exbbt9uxjf9c2cdh1vyx4kfbi4ky1jz-28haocvmk8pow6c0te1lh4dk5 192.168.1.243:2377
This node joined a swarm as a worker.





you can list nodes with this command  ( only you can run command on swarm manager )

rancher@rancher:~$ docker node ls
ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS      ENGINE VERSION
4sm9gzlb14dmz5d6c5qsaxwkj     rancher             Ready               Active                                  19.03.15
y8dw61gd0doujh2mxlfdmm20f *   rancher             Ready               Active              Leader              19.03.15
rancher@rancher:~$





it will not run on worker node

rancher@rancher:~$ docker node ls
Error response from daemon: This node is not a swarm manager. Worker nodes can't be used to view or modify cluster state. Please run this command on a manager node or promote the current node to a manager.





bunu manager swarmda calisririyourz.

rancher@rancher:~$ docker service ls
ID                  NAME                MODE                REPLICAS            IMAGE               PORTS





bunuda worker nodeda

rancher@rancher:~$ docker service ls
Error response from daemon: This node is not a swarm manager. Worker nodes can't be used to view or modify cluster state. Please run this command on a manager node or promote the current node to a manager.





lets create a container for visualizer. on manager swarm. this is easier way to monitor swarm.

docker run -it -d -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock dockersamples/visualizer




http://192.168.1.243:8080/
we cannot see any service running on any node.lets create a service.





docker service create --name nginxweb -p 8081:80 nginx



http://192.168.1.243:8081/
now we can reach nginx page


we can list service running
rancher@rancher:~$ docker service ls
ID                  NAME                MODE                REPLICAS            IMAGE               PORTS
8te03agjmqj1        nginxweb            replicated          1/1                 nginx:latest        *:8081->80/tcp



lets create new service with 4 replika
docker service create --name nginxnewweb -p 8082:80 --replicas 4 nginx



now docker loadbalance containers with diffrent nodes.

rancher@rancher:~$ docker ps
CONTAINER ID        IMAGE                      COMMAND                  CREATED             STATUS                    PORTS                    NAMES
d3d378daafbf        nginx:latest               "/docker-entrypoint.…"   3 minutes ago       Up 3 minutes              80/tcp                   nginxnewweb.3.xkljl0lx932uu10h15ng8umvy
4c2da9dcfd52        nginx:latest               "/docker-entrypoint.…"   3 minutes ago       Up 3 minutes              80/tcp                   nginxnewweb.1.yueecnw7e3qnxeqpoo49ew01v
90772ebcb7e7        nginx:latest               "/docker-entrypoint.…"   9 minutes ago       Up 9 minutes              80/tcp                   nginxweb.1.w5vd8kwus991wwbnljmzzqlys
383d7d2bdfc1        dockersamples/visualizer   "/sbin/tini -- node …"   13 minutes ago      Up 13 minutes (healthy)   0.0.0.0:8080->8080/tcp   quirky_kilby
rancher@rancher:~$


rancher@rancher:~$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
b6bacdcced53        nginx:latest        "/docker-entrypoint.…"   3 minutes ago       Up 3 minutes        80/tcp              nginxnewweb.2.3yo89ba8r38nevfqf72ynfahy
972037f1b509        nginx:latest        "/docker-entrypoint.…"   3 minutes ago       Up 3 minutes        80/tcp              nginxnewweb.4.qedycq654mnq2ujq3cm3xvgfx
rancher@rancher:~$










lets use alpine image and ping google. with 5 replikas
docker service create --name Alpine --replicas 5 alpine ping www.google.com


rancher@rancher:~$ docker service ls
ID                  NAME                MODE                REPLICAS            IMAGE               PORTS
rzuceafkuwn6        Alpine              replicated          5/5                 alpine:latest
5bd7l1757cnp        nginxnewweb         replicated          4/4                 nginx:latest        *:8082->80/tcp
8te03agjmqj1        nginxweb            replicated          1/1                 nginx:latest        *:8081->80/tcp




rancher@rancher:~$ docker ps
CONTAINER ID        IMAGE                      COMMAND                  CREATED              STATUS                    PORTS                    NAMES
e652147e4c54        alpine:latest              "ping www.google.com"    About a minute ago   Up About a minute                                  Alpine.5.             4460i9faf4uivs0vjmi5fd1w0
87c2c092c337        alpine:latest              "ping www.google.com"    About a minute ago   Up About a minute                                  Alpine.3.             0579o9nx3v017ynszcer10cww
d3d378daafbf        nginx:latest               "/docker-entrypoint.…"   7 minutes ago        Up 7 minutes              80/tcp                   nginxneww             eb.3.xkljl0lx932uu10h15ng8umvy
4c2da9dcfd52        nginx:latest               "/docker-entrypoint.…"   7 minutes ago        Up 7 minutes              80/tcp                   nginxneww             eb.1.yueecnw7e3qnxeqpoo49ew01v
90772ebcb7e7        nginx:latest               "/docker-entrypoint.…"   13 minutes ago       Up 13 minutes             80/tcp                   nginxweb.             1.w5vd8kwus991wwbnljmzzqlys
383d7d2bdfc1        dockersamples/visualizer   "/sbin/tini -- node …"   18 minutes ago       Up 18 minutes (healthy)   0.0.0.0:8080->8080/tcp   quirky_ki             lby


rancher@rancher:~$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
a771d0c23cd3        alpine:latest       "ping www.google.com"    2 minutes ago       Up About a minute                       Alpine.2.qss6ka7qzbsqexagcxe0d1fh4
71be688f5bf9        alpine:latest       "ping www.google.com"    2 minutes ago       Up About a minute                       Alpine.1.r4f0f56wuwae00zzh4x27n4oc
d6f1f76d3c66        alpine:latest       "ping www.google.com"    2 minutes ago       Up About a minute                       Alpine.4.s3kxfohf6d03v9nyg2giju3hv
b6bacdcced53        nginx:latest        "/docker-entrypoint.…"   7 minutes ago       Up 7 minutes        80/tcp              nginxnewweb.2.3yo89ba8r38nevfqf72ynfahy
972037f1b509        nginx:latest        "/docker-entrypoint.…"   7 minutes ago       Up 7 minutes        80/tcp              nginxnewweb.4.qedycq654mnq2ujq3cm3xvgfx






as we see when we create service automatically loadbalancing
rancher@rancher:~$ docker service ps Alpine
ID                  NAME                IMAGE               NODE                DESIRED STATE       CURRENT STATE           ERROR               PORTS
r4f0f56wuwae        Alpine.1            alpine:latest       rancher             Running             Running 4 minutes ago
qss6ka7qzbsq        Alpine.2            alpine:latest       rancher             Running             Running 4 minutes ago
0579o9nx3v01        Alpine.3            alpine:latest       rancher             Running             Running 4 minutes ago
s3kxfohf6d03        Alpine.4            alpine:latest       rancher             Running             Running 4 minutes ago
4460i9faf4ui        Alpine.5            alpine:latest       rancher             Running             Running 4 minutes ago



rancher@rancher:~$ docker service ps nginxnewweb
ID                  NAME                IMAGE               NODE                DESIRED STATE       CURRENT STATE            ERROR               PORTS
yueecnw7e3qn        nginxnewweb.1       nginx:latest        rancher             Running             Running 11 minutes ago
3yo89ba8r38n        nginxnewweb.2       nginx:latest        rancher             Running             Running 11 minutes ago
xkljl0lx932u        nginxnewweb.3       nginx:latest        rancher             Running             Running 11 minutes ago
qedycq654mnq        nginxnewweb.4       nginx:latest        rancher             Running             Running 11 minutes ago




rancher@rancher:~$ docker service scale nginxnewweb=6
visualisera gittigimzde 6 tane replikaya ciktigini gorebiliriz.

rancher@rancher:~$ docker service scale nginxweb=2
ayni sekilde nginxwebinde 2 ye ciktignin gorebiliriz.

rancher@rancher:~$ docker service ls
ID                  NAME                MODE                REPLICAS            IMAGE               PORTS
rzuceafkuwn6        Alpine              replicated          5/5                 alpine:latest
5bd7l1757cnp        nginxnewweb         replicated          6/6                 nginx:latest        *:8082->80/tcp
8te03agjmqj1        nginxweb            replicated          2/2                 nginx:latest        *:8081->80/tcp




rancher@rancher:~$ docker service scale Alpine=2
we can scale down with this way



rancher@rancher:~$ docker service scale nginxnewweb=2
for other container as well now if we check we see that only 2 left on diffrent nodes for each containers.


rancher@rancher:~$ docker service ls
ID                  NAME                MODE                REPLICAS            IMAGE               PORTS
rzuceafkuwn6        Alpine              replicated          2/2                 alpine:latest
5bd7l1757cnp        nginxnewweb         replicated          2/2                 nginx:latest        *:8082->80/tcp
8te03agjmqj1        nginxweb            replicated          2/2                 nginx:latest        *:8081->80/tcp











now lets drain one of node.

rancher@rancher:~$ docker node ls
ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS      ENGINE VERSION
4sm9gzlb14dmz5d6c5qsaxwkj     rancher             Ready               Active                                  19.03.15
y8dw61gd0doujh2mxlfdmm20f *   rancher             Ready               Active              Leader              19.03.15



rancher@rancher:~$ docker node update --availability drain 4sm9gzlb14dmz5d6c5qsaxwkj


rancher@rancher:~$ docker ps
CONTAINER ID        IMAGE                      COMMAND                  CREATED             STATUS                    PORTS                    NAMES
d6cb830073bb        nginx:latest               "/docker-entrypoint.…"   27 seconds ago      Up 21 seconds             80/tcp                   nginxnewweb.2.zbyhdmveq5keciv4uxpcp0oe3
eb53d92cf3ea        alpine:latest              "ping www.google.com"    27 seconds ago      Up 15 seconds                                      Alpine.1.sodro1w21cvvykdwm9td6clhy
9ca8bc942a62        nginx:latest               "/docker-entrypoint.…"   27 seconds ago      Up 22 seconds             80/tcp                   nginxweb.2.iyyvpm75yetn6y799cn409xq7
87c2c092c337        alpine:latest              "ping www.google.com"    23 minutes ago      Up 23 minutes                                      Alpine.3.0579o9nx3v017ynszcer10cww
4c2da9dcfd52        nginx:latest               "/docker-entrypoint.…"   28 minutes ago      Up 28 minutes             80/tcp                   nginxnewweb.1.yueecnw7e3qnxeqpoo49ew01v
90772ebcb7e7        nginx:latest               "/docker-entrypoint.…"   34 minutes ago      Up 34 minutes             80/tcp                   nginxweb.1.w5vd8kwus991wwbnljmzzqlys
383d7d2bdfc1        dockersamples/visualizer   "/sbin/tini -- node …"   39 minutes ago      Up 39 minutes (healthy)   0.0.0.0:8080->8080/tcp   quirky_kilby

rancher@rancher:~$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES


now all nodes working on management swarm.worker node drained.







rancher@rancher:~$ docker node update --availability active 4sm9gzlb14dmz5d6c5qsaxwkj
bu sekilde tekrar aktif edebiliriz.



rancher@rancher:~$ docker service scale nginxnewweb=3
servislerden birini cogalttigimzda diger nodada gececegini gorecegiz.2 tane zaten tek nodda calisiyordu.3.su worker noda gececektir.visualizeerdanda bunu gorebiliriz.

rancher@rancher:~$ docker service ps nginxnewweb
ID                  NAME                IMAGE               NODE                DESIRED STATE       CURRENT STATE            ERROR               PORTS
yueecnw7e3qn        nginxnewweb.1       nginx:latest        rancher             Running             Running 33 minutes ago
zbyhdmveq5ke        nginxnewweb.2       nginx:latest        rancher             Running             Running 5 minutes ago
3yo89ba8r38n         \_ nginxnewweb.2   nginx:latest        rancher             Shutdown            Shutdown 5 minutes ago
t6f6ltt8gr0a        nginxnewweb.3       nginx:latest        rancher             Running             Running 2 minutes ago




rancher@rancher:~$ docker node update --availability drain y8dw61gd0doujh2mxlfdmm20f
dogru olani bunu sadece manager nodda yapmaktir.cunku nodelarin managerde calismasini istemeyiz.



rancher@rancher:~$ docker service scale nginxweb=6
6 replika aldigimzda artik tum nodlarin workerda calistigini ve managerde hic node calismadigini gorecegiz.




docker swarm used for zero downtime high availibility.







ingress network:
when we create docker swarm we are running ingress network

docker run -p 80:5000 my-web-server

docker service create \
--replicas=2 \
-p 80:5000 \
my-web-server



ingress network in fact type of overlay network meaning single network that bounce all nodes in cluster.

the way load balancer work, receives any node in the cluster and forward that request to the respective instences any other route creating routing mesh.
this is default docker swarm behavior. we dont need to do any addtional configuration.

create service
number replica
publish port

docker swarm be unsure instances published all the nodes and users can access the services using the ip of any of the nodes. when they do traffic routed right services internally.




all container docker host has name of container.dns resolve eachother container name.
cuz each restart node can assign diffrent ip address. thats why they use dns address as container name.

```
***
