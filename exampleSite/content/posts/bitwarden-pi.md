+++
title = "Bitwarden Raspberry Docker CLI and Docker Compose"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-16T05:00:00Z
description = "bitwarden raspberry docker"
categories = ["technology"]
type = "post"

+++
#### Docker CLI:

```
sudo docker pull bitwardenrs/server:latest
sudo docker run -d --name bitwarden -v /srv/dev-disk-by-label-Files/Config/BitwardenRS/:/data/ -p 8100:80 bitwardenrs/server:latest
```

#### Docker Compose:

```
version: "2"
services:
  bitwardenrs:
    image: bitwardenrs/server:latest
    container_name: bitwardenrs
    volumes:
      - /srv/dev-disk-by-label-Files/Config/BitWardenRS:/data/
    ports:
      - 8100:80
    restart: unless-stopped
```