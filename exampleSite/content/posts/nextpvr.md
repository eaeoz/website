+++
title = "nextpvr docker compose"
image = "/images/post/nextpvr.jpg"
author = "Sedat"
date = "2025-02-24T00:02:04Z"
description = "nextpvr docker compose"
categories = ["Docker"]
type = "post"

+++

NextPVR is a whole-home digital video recorder. The NextPVR server can be installed on Windows, Linux, Mac or Docker. Clients are available for a wide range of devices, allowing you access recordings and live TV throughout your home. Supports most devices. DVB, ATSC, QAM, DMB-T, Analog, SAT>IP, HDPVR, and Copy-Freely CableCard. Provides an easy to use, easy to understand, TV friendly user interface for the whole family. Includes all the TV functions you'd expect... Live TV, TV Guide, Recordings, Search, Web Scheduler. We care for our users, and will do everything we can to ensure things continue to run smoothly.

***

- [Click here for more information.](https://hub.docker.com/r/nextpvr/nextpvr_amd64)

**Docker compose:**
```
version: "3"
services:
  nextpvr:
    image: nextpvr/nextpvr_amd64:stable
    container_name: nextpvr
    restart: unless-stopped
    networks:
      - default
    ports:
      - "8866:8866"  # Web UI
      - "16891:16891/udp"  # For NextPVR network discovery
    volumes:
      - ./nextpvr_config:/config
      - ./videos:/recordings
      - ./videos:/buffer
networks:
  default:
    driver: bridge
```
***

- *To access to ui:*
`http://<hostip>:8866/`

admin/password
