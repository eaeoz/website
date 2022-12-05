+++
title = "Calibre Web - Self Hosted Book Archive Docker Compose"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-16T05:00:00Z
description = "calibre web docker"
categories = ["docker"]
type = "post"

+++
#### Docker Compose:

```
version: "2"
services:
  calibre-web:
    image: lscr.io/linuxserver/calibre-web
    container_name: calibre-web
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Istanbul
      - DOCKER_MODS=linuxserver/calibre-web:calibre #optional
      - OAUTHLIB_RELAX_TOKEN_SCOPE=1 #optional
    volumes:
      - /docker/calibre2/data:/config
      - /docker/calibre2/library:/books
    ports:
      - 8994:8083
    restart: unless-stopped
```

transfer metadata.db under books folder from docker shell. use wget to transfer and give 777 mod permission or transfer to books folder and give permission from bash

- admin > edit basic configuration > enable uploads

- swithc to darkmode from settings and disable all sidebars

- admin > edit user settings > allow ebook viewer that you can view on browser