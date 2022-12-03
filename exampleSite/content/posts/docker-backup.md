+++
title = "Docker Image Backup With Container Volumes"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-11T05:00:00Z
description = "docker backup volume"
categories = ["technology"]
type = "post"

+++
`sudo docker ps`

`sudo docker inspect <name>`

copy under mounts > source sections
if more then one copy both

`sudo docker stop <name>`

make sure docker stopped

`sudo docker ps -a`

and copy <container id>
```
sudo docker commit <container id> <give a name exp:piholebackup>

```

`sudo docker images`

now we see image created name piholebackup

`sudo docker save piholebackup > piholeback.tar`

```
ls
piholeback.tar
```

from another computer first transfer tar file via ftp, ssh or scp kind way and type on command (same time transfer sources section folders)

and run this command from new computer

`docker load -i piholeback.tar`

list images which is impoerted

`docker images`

*Now before running container we need to add volumes as well. For that manually copy volumes where you target on your local machine and paste it same location on your new pc. Now we use that volume source as docker volumes. We target same target when we deploy new docker container.*

Example Nginx Proxy Manager Backup with volumes:

`sudo docker inspect nginxproxy`

```
  "Mounts": [
            {
                "Type": "bind",
                "Source": "/docker/appdata/nginx-proxy-manager",
                "Destination": "/config",
                "Mode": "rw",
                "RW": true,
                "Propagation": "rprivate"
            }
        ],n": "rprivate"
```

we got the volume information, we should copy on the recent computer files same as here on the source specified section.

destination section inside the container it will be running as same.

```
                "Source": "/docker/appdata/nginx-proxy-manager",
                "Destination": "/config",
```

now lets deploy the application:

`docker run -d --name nginxproxy -p 443:4443 -p 80:8080 -p 81:8181 -v "/docker/appdata/nginx-proxy-manager/:/config/" --dns=127.0.0.1 --dns=1.1.1.1 --restart=unless-stopped nginxproxy`

if more then one volumes we need to add more volume parameters with -v flag.

> If application not deployed with volume information, you should check under /var/lib/docker/overlay2 folder.

