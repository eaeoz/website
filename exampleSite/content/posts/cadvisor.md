+++
title = "Cadvisor for Docker Monitoring Data"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-16T05:00:00Z
description = "cadvisor docker monitor"
categories = ["docker"]
type = "post"

+++
```
version: "2.1"
services:
  cadvisor123:
    image: gcr.io/cadvisor/cadvisor:latest
    container_name: cadvisor123
    volumes:
      - /:/rootfs:ro
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - /var/run:/var/run:rw
      - /sys:/sys:ro
      - /var/lib/docker:/var/lib/docker:ro
      - /sys/fs/cgroup:/cgroup:ro
      - /dev/disk/:/dev/disk:ro
    command:
      - '-housekeeping_interval=10s'
      - '-docker_only=true'
    restart: unless-stopped
    devices:
      - /dev/kmsg:/dev/kmsg
    security_opt:
      - no-new-privileges:true
    ports:
      - 3015:8080
    labels:
      org.label-schema.group: "monitoring"
```

or

```
version: "2.1"
services:
  cadvisor:
    image: gcr.io/cadvisor/cadvisor:latest
    container_name: cadvisor
    privileged: true
    devices:
      - /dev/kmsg:/dev/kmsg
    ports:
      - 3019:8080 #change as necessary
    volumes:
      - /:/rootfs:ro
      - /var/run:/var/run:ro
      - /sys:/sys:ro
      - /var/lib/docker/:/var/lib/docker:ro
      - /dev/disk/:/dev/disk:ro
    restart: unless-stopped
```