+++
title = "Bitnami Moodle - Online Course Management"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-16T05:00:00Z
description = "online course moodle"
categories = ["docker"]
type = "post"

+++
#### Installation

```
curl -sSL https://raw.githubusercontent.com/bitnami/bitnami-docker-moodle/master/docker-compose.yml > docker-compose.yml
docker-compose up -d
```

Docker Compose File

```
version: '2'
services:
  mariadb:
    image: docker.io/bitnami/mariadb:10.6
    environment:
      # ALLOW_EMPTY_PASSWORD is recommended only for development.
      - ALLOW_EMPTY_PASSWORD=yes
      - MARIADB_USER=bn_moodle
      - MARIADB_DATABASE=bitnami_moodle
      - MARIADB_CHARACTER_SET=utf8mb4
      - MARIADB_COLLATE=utf8mb4_unicode_ci
    volumes:
      - 'mariadb_data:/bitnami/mariadb'
  moodle:
    image: docker.io/bitnami/moodle:4
    ports:
      - '80:8080'
      - '443:8443'
    environment:
      - MOODLE_DATABASE_HOST=mariadb
      - MOODLE_DATABASE_PORT_NUMBER=3306
      - MOODLE_DATABASE_USER=bn_moodle
      - MOODLE_DATABASE_NAME=bitnami_moodle
      # ALLOW_EMPTY_PASSWORD is recommended only for development.
      - ALLOW_EMPTY_PASSWORD=yes
    volumes:
      - 'moodle_data:/bitnami/moodle'
      - 'moodledata_data:/bitnami/moodledata'
    depends_on:
      - mariadb
volumes:
  mariadb_data:
    driver: local
  moodle_data:
    driver: local
  moodledata_data:
    driver: local
```

`Username: user`

`Password: bitnami`

or

```
version: '2'
services:
  mariadb:
    image: mariadb
    volumes:
      - /srv/Configs/Databases/Moodle:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=moodle
      - MYSQL_ROOT_USER=root
      - MYSQL_DATABASE=moodle
      
  moodle:
    image: bitnami/moodle:latest
    ports:
      - 8080:8080
      - 8443:8443
    environment:
      - MOODLE_DATABASE_HOST=mariadb
      - MOODLE_DATABASE_USER=root
      - MOODLE_DATABASE_PASSWORD=moodle
      - MOODLE_DATABASE_NAME=moodle
      - PUID=998
      - PGID=100
    volumes:
      - /srv/Configs/Moodle:/bitnami/moodle
      - /srv/Configs/MoodleData:/bitnami/moodledata
    depends_on:
      - mariadb
    links:
      - mariadb:mariadb
```

in container bash for settings:

```
root@d4bb39b8a40a:/bitnami/moodle# nano config-dist.php
```



repo:

https://github.com/bitnami/bitnami-docker-moodle