+++
title = "plex media server docker compose"
image = "/images/post/plex.jpg"
author = "Sedat"
date = "2025-02-24T00:02:06Z"
description = "plex docker compose"
categories = ["Docker"]
type = "post"

+++
Plex is a powerful media server that allows users to organize, stream, and access their personal media library from any device. It supports movies, TV shows, music, and photos, offering an intuitive interface with metadata, cover art, and detailed information for a seamless viewing experience. Plex can transcode media on the fly, ensuring compatibility across different devices, from smartphones and smart TVs to gaming consoles and web browsers. It also supports remote access, allowing users to stream their content from anywhere. Additionally, with integrations like Plex Pass, users can enjoy premium features such as offline downloads, hardware-accelerated transcoding, and live TV with DVR functionality. Whether running on a local machine, a Docker container, or a dedicated NAS, Plex is an excellent solution for centralized media management.

***

- [Click here for more information.](https://hub.docker.com/r/plexinc/pms-docker/)

**Docker compose:**
```
version: '3.8'
services:
  plex:
    image: plexinc/pms-docker:latest             # Official Plex Media Server image
    container_name: plex
    environment:
      - PLEX_CLAIM=claim-PKvnnwAVqwPasdasdddP    # Optional for linking to your Plex account
      - TZ=Europe/Istanbul      # Example: America/New_York
    volumes:
      - /docker/plex/config:/config    # Configuration files
      - /docker/plex/transcode:/transcode  # Temporary transcoding files
      - /shared/Media:/data       # Media files (e.g., movies, TV shows, music)
    restart: unless-stopped
    networks:
      ipnet:
        ipv4_address: 192.168.10.3
    dns:
      - 1.1.1.1    # Cloudflare's DNS
      - 8.8.8.8    # Google's DNS
networks:
  ipnet:
    external: true
```
***

- *To access to ui:*
`http://<host-ip>:32400/web`

- *To get claim token:* [Click here](https://www.plex.tv/claim/)
