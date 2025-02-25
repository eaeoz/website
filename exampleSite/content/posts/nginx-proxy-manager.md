+++
title = "nginx proxy manager docker run command"
image = "/images/post/nginx-proxy-manager.jpg"
author = "Sedat"
date = "2025-02-24T00:02:09Z"
description = "nginx proxy manager"
categories = ["Docker"]
type = "post"

+++

Deploying Nginx Proxy Manager using a docker run command provides a simple and quick way to set up a reverse proxy with an intuitive web interface for managing SSL certificates, redirects, and access control. Nginx Proxy Manager simplifies the process of routing traffic to self-hosted services while securing them with Let's Encrypt SSL certificates. To run it as a standalone container, the docker run command must define necessary environment variables, volumes for persistent data storage, and network settings. A typical command includes mounting configuration files, database storage, and specifying ports (80, 81, and 443). While docker run works for quick deployment, using Docker Compose is recommended for easier management and scalability, especially when integrating a database like MariaDB for persistent configurations.

***

- [Click here for more information.](https://github.com/jlesage/docker-nginx-proxy-manager)

**Docker compose:**

```
sudo docker run -d \
--name=nginx-proxy-manager \
-e PUID=998 \
-e PGID=100 \
-p 81:8181 \
-p 80:8080 \
-p 443:4443 \
-v /docker/nginx-proxy-manager:/config:rw \
jlesage/nginx-proxy-manager
```

***

- *Access to the ui:*

`http://<hostip>:81/`

username: admin@example.com

password: changeme

***

**To manage subdomains using a Cloudflared tunnel with the Nginx Proxy Manager UI (locally instead of the Cloudflare web page), only specific versions of the tunnel container work with this configuration. For example, the tested and verified version is cloudflared:2022.4.0-amd64.**

```
- set nginx docker cloudflred listening port to 8001

 login to nginx-proxy-manager bash set listening port to 8001:
nano /etc/nginx/conf.d/default.conf





- and tunnel container yml configuration endpoint port to 4443 (instead 443), replace tunnelid with your actual tunnelid (and nginx-proxy-manager-ip), now we going to do this configruation:



(grant access for shell)
sudo -i

(create folder for cloudflared tunnel config files and give access permissions)
mkdir -p /mnt/user/appdata/cloudflared/ && chmod -R 777 /mnt/user/appdata/cloudflared/

docker run -it --rm -v /mnt/user/appdata/cloudflared:/home/nonroot/.cloudflared/ cloudflare/cloudflared:2022.4.0-amd64 tunnel login
(select domain which you want to use for tunnel from the opening url)

(create tunnel)
docker run -it --rm -v /mnt/user/appdata/cloudflared:/home/nonroot/.cloudflared/ cloudflare/cloudflared:2022.4.0-amd64 tunnel create TUNNEL1

output message: Created tunnel TUNNEL1 with id tunnelid



type:

nano /mnt/user/appdata/cloudflared/config.yml


then edit:

tunnel: tunnelid
credentials-file: /root/.cloudflared/tunnelid.json

ingress:
  - service: https://<nginx-proxy-manager-ip>:4443
    originRequest:
      originServerName: mywebsite.com




type:

cd /mnt/user/appdata/cloudflared
ls

output message: tunnelid.json  cert.pem  config.yml



- redirect cname of your root domain from dns settins like: tunnelid.cfargotunnel.com



- run tunnel

version: '2'
services:
    nginx:
        image: nginx
    cloudflared:
        image: cloudflare/cloudflared:2022.4.0-amd64
        user: root
        command: 'tunnel run'
        volumes:
            - /mnt/user/appdata/cloudflared:/root/.cloudflared
        restart: unless-stopped






- run container:

sudo docker run -d \
--name=nginx-proxy-manager \
-e PUID=998 \
-e PGID=100 \
-p 81:8181 \
-p 8001:8080 \
-p 4443:4443 \
-v /docker/appdata/nginx-proxy-manager:/config:rw \
jlesage/nginx-proxy-manager
```
