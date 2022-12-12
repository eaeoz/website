+++
title = "Dashmachine Docker Compose"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2022-11-11T05:00:00Z
description = "dashmachine docker compose"
categories = ["docker"]
type = "post"

+++
```
version: "2.1"
services:
  dashmachine:
    image: rmountjoy/dashmachine0.7:latest
    container_name: dashmachine
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Detroit
      - EDITOR_URL=https://your-reverse-proxy.url
    volumes:
      - /config/directory:/DashMachine/config
    ports:
      - 5000:5000
    restart: unless-stopped
  code-server:
    image: linuxserver/code-server:latest
    container_name: code-server
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Detroit
      - PASSWORD=mysecretpassword
      - SUDO_PASSWORD=mysecretpassword
      - PROXY_DOMAIN=your-reverse-proxy.url
    volumes:
      - /config/directory:/config
      - /config/directory/workspace:/config/workspace/Dashmachine
    ports:
      - 8443:8443
    restart: unless-stopped
```