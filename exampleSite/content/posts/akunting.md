+++
title = "Akaunting docker-compose"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-07T05:00:00Z
description = "akunting docker"
categories = ["technology"]
type = "post"

+++
```
version: '2.1'

services:

  akaunting:
    image: kuralabs/docker-akaunting:latest
    restart: always
    ports:
      - 3017:8080
    environment:
      MYSQL_ROOT_PASSWORD: snBq^nxhB^vL49C56JVuvx
    volumes:
      - /docker/akaunting/mysql:/var/lib/mysql
      - /docker/akaunting/logs:/var/log
      - /docker/akaunting/config:/var/www/akaunting/config
```

for mysql password generate with bitwarden
22 character with numerical, special characters, capital and noromal
example:

9G!ixfCB7t@!*Gd8hTi9PY

durin installation check docker logs from portainer interface and paste to installation window

```
IMPORTANT!! GO TO THE WEB INTERFACE TO FINISH INSTALLATION!
Use the following parameters in 'Database Setup':
Hostname:     127.0.0.1:3306
Username:     akaunting
Password:     RrNQpw+MxKE/oyJjpMKzmDs+ewP/KAeqr3Meu5Rp7fo=
Database:     akaunting
Please securely store these credentials!
```










