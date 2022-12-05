+++
title = "Appsmith docker-compose"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-11T05:00:00Z
description = "appsmith docker"
categories = ["docker"]
type = "post"

+++
```
version: "3"

services:
  appsmith:
    image: index.docker.io/appsmith/appsmith-ce
    container_name: appsmith
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./stacks:/appsmith-stacks
    restart: unless-stopped
  #   # Uncomment the lines below to enable auto-update
  #   labels:
  #     com.centurylinklabs.watchtower.enable: "true"

  # auto_update:
  #   image: containrrr/watchtower:latest-dev
  #   volumes:
  #     - /var/run/docker.sock:/var/run/docker.sock
  #   # Update check interval in seconds.
  #   command: --schedule "0 0 * ? * *" --label-enable --cleanup
  #   restart: unless-stopped
```