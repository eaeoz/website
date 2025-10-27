+++
title = "Samba Docker Compose"
image = "/images/post/samba.jpg"
author = "Sedat"
date = "2025-02-24T00:02:10Z"
description = "samba docker compose"
categories = ["Docker"]
type = "post"

+++

Running Samba in a Docker environment provides a flexible and efficient way to set up a file-sharing server that supports SMB (Server Message Block) protocol for Windows, Linux, and macOS clients. By containerizing Samba, users can isolate configurations, easily manage updates, and deploy it across different systems without modifying the host. A Docker container running Samba allows seamless sharing of directories while maintaining access controls, authentication, and network visibility. With Docker Compose, users can define persistent storage for shared volumes and configure environment variables for user credentials and permissions. This setup is ideal for self-hosted NAS solutions, team collaboration, or home network file sharing, ensuring a lightweight and manageable deployment.

***

- [Click here for more information.](https://github.com/crazy-max/docker-samba)

### Instructions

**create folder for environment first:**

```
mkdir compose
cd compose
mkdir smb
cd smb
mkdir data
```

**create compose file:**

`nano docker-compose.yml`

```
version: "2"
services:
  samba:
    image: crazymax/samba
    container_name: samba
    network_mode: host
    volumes:
      - "./data:/data" # Contains cache, configuration and runtime data
      - "/shared:/samba/HDD"
      - "/jellyfin/Music:/samba/Music"
      - "/videos:/samba/videos"
    #  - "./share:/samba/share" - optional additional share - see config.yml for permissions
    #  - "./foo:/samba/foo" - optional additional share - see config.yml for permissions
    #  - "./foo-baz:/samba/foo-baz" - optional additional share - see config.yml for permissions
    environment:
      - "TZ=Europe/Istanbul"
    #  - "CONFIG_FILE=/your-location" this can be anywhere you want. Default is /data
    #  - "SAMBA_WORKGROUP=WORKGROUP" change to your workgroup, default it WORKGROUP
    #  - "SAMBA_SERVER_STRING=some string" is the equivalent of the NT Description field
      - "SAMBA_LOG_LEVEL=0"
    #  - "SAMBA_FOLLOW_SYMLINKS=NO" default is yes
    #  - "SAMBA_WIDE_LINKS=NO" default is yes
    #  - "SAMBA_HOSTS_ALLOW=0.0.0.0/0" default 127.0.0.0/8 10.0.0.0/8 172.16.0.0/12 192.168.0.0/16
    #  - "SAMBA_INTERFACES=some-interface" default all
    #  - "WSDD2_ENABLE=1" default is 0
    #  - "WSDD2_HOSTNAME=string" Override hostname (default to host or container name)
    #  - "WSDD2_NETBIOS_NAME=some-name" Set NetBIOS name (default to hostname)
    #  - "WSDD2_INTERFANCE=interface-name" Reply only on this interface
    restart: unless-stopped
```

**create config file**

```
cd data

nano config.yml
```

```
auth:
  - user: sedat
    group: sedat
    uid: 1000
    gid: 1000
    password: password
  - user: sedat2
    group: sedat2
    uid: 1001
    gid: 1001
    password: password # password_file: /run/secrets/baz_password # you can use this instead of password

global:
  - "force user = sedat"
  - "force group = sedat"

share:
  - name: Harddrive
    comment: HDD
    path: /samba/HDD
    browsable: yes
    readonly: no
    guestok: yes
    veto: no
    recycle: yes
  - name: Music
    path: /samba/Music
    browsable: yes
    readonly: no
    guestok: yes
    veto: no
    recycle: yes
  - name: Videos
    path: /samba/videos
    browsable: yes
    readonly: no
    guestok: yes
    veto: no
    recycle: yes
```
