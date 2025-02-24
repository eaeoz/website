+++
title = "qbittorrent radarr prowlarr stack - docker compose"
image = "/images/post/radarr.jpg"
author = "Sedat"
date = "2025-02-24T00:02:05Z"
description = "qbittorrent radarr prowlarr"
categories = ["Docker"]
type = "post"

+++
Running qBittorrent, Radarr, and Prowlarr in a Docker stack is an efficient way to automate media management. qBittorrent is an open-source torrent client known for its speed and extensive feature set, while Radarr is a PVR (Personal Video Recorder) designed to manage movie collections. Prowlarr acts as an indexer manager, integrating with Radarr to provide torrent and Usenet indexer sources. By configuring these applications within a docker-compose.yml file, they can seamlessly communicate within the same network. Radarr fetches indexer information from Prowlarr, identifies missing movies, and sends download requests to qBittorrent, creating a fully automated media acquisition and management workflow. Running them in a Docker environment simplifies updates, maintenance, and resource management, ensuring a streamlined and efficient setup.


***

- [Click here for more information.](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://github.com/qbittorrent/qBittorrent)

##### Docker compose:
```
version: '3.7'
services:
  qbittorrent:
    image: lscr.io/linuxserver/qbittorrent:latest
    container_name: tor
    environment:
      - PUID=1001
      - PGID=1001
      - TZ=Europe/Istanbul
      - WEBUI_PORT=8085
    volumes:
      - /docker/tor:/config
      - /shared/Media/Movies:/downloads
    ports:
      - 6881:6881
      - 6881:6881/udp
      - 8085:8085
    restart: unless-stopped
    dns:
      - 1.1.1.1
      - 8.8.8.8
  prowlarr:
    image: lscr.io/linuxserver/prowlarr:latest
    container_name: prowlarr
    environment:
      - PUID=1001
      - PGID=1001
      - TZ=Europe/Istanbul
    volumes:
      - /docker/prowlarr/config:/config
      - /etc/localtime:/etc/localtime:ro
    ports:
      - 9696:9696
    restart: unless-stopped
    dns:
      - 1.1.1.1
      - 8.8.8.8
  radarr:
    image: linuxserver/radarr
    container_name: radarr
    environment:
      - PUID=1001
      - PGID=1001
      - TZ=Europe/Istanbul
    volumes:
      - /docker/radarr/config:/config
      - /shared/Media/Movies:/movies
      - /docker/radarr/torrent:/downloads
    ports:
      - 7878:7878
    restart: unless-stopped
    dns:
      - 1.1.1.1
      - 8.8.8.8
networks:
  default:
    driver: bridge
```
***


- To access to qBittorrent ui:
`http://<hostip>:8866/`

admin/admin

- To access to Prowlarr ui:
`http://<hostip>:9696/`

- To access to Radarr ui:
`http://<hostip>:7878/`
