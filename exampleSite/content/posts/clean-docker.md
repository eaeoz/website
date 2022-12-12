+++
title = "Clean Docker Unused Images, Containers and Networks"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2022-12-12T05:00:00Z
description = "docker clean"
categories = ["docker"]
type = "post"

+++
*before run commands below make sure all containers are running.*

sudo docker system prune --volumes
sudo docker image prune -a
sudo docker network prune