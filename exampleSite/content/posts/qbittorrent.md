+++
title = "Qbittorrent Radarr Prowlarr Stack"
image = "/images/post/radarr.jpg"
author = "Sedat"
date = "2025-10-24T00:02:56Z"
description = "qbittorrent radarr prowlarr"
categories = ["Docker"]
type = "post"

+++

Running qBittorrent, Radarr, and Prowlarr in a Docker stack is an efficient way to automate media management. qBittorrent is an open-source torrent client known for its speed and extensive feature set, while Radarr is a PVR (Personal Video Recorder) designed to manage movie collections. Prowlarr acts as an indexer manager, integrating with Radarr to provide torrent and Usenet indexer sources. By configuring these applications within a docker-compose.yml file, they can seamlessly communicate within the same network. Radarr fetches indexer information from Prowlarr, identifies missing movies, and sends download requests to qBittorrent, creating a fully automated media acquisition and management workflow. Running them in a Docker environment simplifies updates, maintenance, and resource management, ensuring a streamlined and efficient setup.


***

- [Click here for more information.](https://github.com/qbittorrent/qBittorrent)

**Docker compose:**
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


- Access to qBittorrent ui:

`http://<hostip>:8866/`

admin/admin

- Access to Prowlarr ui:

`http://<hostip>:9696/`

- Access to Radarr ui:

`http://<hostip>:7878/`


---

**Other containers can be used with this stack:**

- jackett instead prowlarr (indexer)

- sonarr (for tv shows)

- lazyLibrarian (ebook)

- lidarr (music)

- readarr (books and comic)

***

(not listed)

- mylar (comicbook)

- whisparr (audiobook)

**Examples for the containers specified above:**

```
version: '3.7'
services:
  jackett:
    image: linuxserver/jackett
    container_name: jackett
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Istanbul
      volumes:
      - /docker/jackett/config:/config
      - /etc/localtime:/etc/localtime:ro
      ports:
      - 9117:9117
      restart: unless-stopped
  sonarr:
    image: linuxserver/sonarr
    container_name: sonarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Istanbul
    volumes:
      - /docker/sonarr/config:/config
      - /docker/sonarr/tv:/tv
      - /downloads/tv:/downloads
    ports:
      - 8989:8989
    restart: unless-stopped
  lazylibrarian:
    image: linuxserver/lazylibrarian
    container_name: lazylibrarian
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Istanbul
    volumes:
      - /docker/lazylibrarian/config:/config
      - /docker/lazyLibrarian/books:/books
      - /downloads/books:/downloads
    ports:
      - 5299:5299
    restart: unless-stopped
  lidarr:
    image: ghcr.io/linuxserver/lidarr
    container_name: lidarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europle/Istanbul
    volumes:
      - /docker/lidarr/config:/config
      - /docker/lidarr/music:/music
      - /downloads/music:/downloads
    ports:
      - 8686:8686
    restart: unless-stopped
  readarr:
    image: lscr.io/linuxserver/readarr:develop
    container_name: readarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Istanbul
    volumes:
      - /docker/readarr/config:/config
      - /docker/readarr/comics:/comics
      - /downloads/comics:/downloads
      - /etc/localtime:/etc/localtime:ro
    ports:
      - 8787:8787
    restart: unless-stopped   
```
