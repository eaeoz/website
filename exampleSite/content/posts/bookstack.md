+++
title = "Bookstack Docker Compose"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-16T05:00:00Z
description = "bookstack docker compose"
categories = ["docker"]
type = "post"

+++
#### Docker Compose:

```
version: "2"
services:
  wiki:
    image: ghcr.io/linuxserver/bookstack
    container_name: wiki
    environment:
      - PUID=998
      - PGID=100
      - APP_URL=http://192.168.1.131:6999
      - DB_HOST=db
      - DB_USER=user
      - DB_PASS=password
      - DB_DATABASE=app
      - APP_DEFAULT_DARK_MODE=true
    volumes:
      - /path/to/config:/config
    ports:
      - 6999:80
    restart: unless-stopped
    depends_on:
      - hwikidb
  
  db:
    image: ghcr.io/linuxserver/mariadb
    container_name: db
    #command: --default-authentication-plugin=mysql_native_password
    ports:
      - 3306:3306
    environment:
      - PUID=998
      - PGID=100
      - MYSQL_ROOT_PASSWORD=password
      - TZ=America/Denver
      - MYSQL_DATABASE=app
      - MYSQL_USER=user
      - MYSQL_PASSWORD=password
    volumes:
      - /path/to/config:/config
    restart: unless-stopped

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    depends_on:
      - db
    environment:
      - PMA_HOST=db
    ports:
      - 9632:80
```

```
Username: admin@admin.com
Password: password
```