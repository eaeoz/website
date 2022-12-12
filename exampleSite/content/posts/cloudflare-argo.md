+++
title = "Cloudflare Argo Tunnel on Docker"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2022-11-11T05:00:00Z
description = "cloudflare argo tunnel"
categories = ["docker"]
type = "post"

+++
#### File Permissions and Creating Tunnel
```
sudo -i

mkdir -p /mnt/user/appdata/cloudflared/ && chmod -R 777 /mnt/user/appdata/cloudflared/
```

select domain which you want to use for tunnel


```
docker run -it --rm -v /mnt/user/appdata/cloudflared:/home/nonroot/.cloudflared/ cloudflare/cloudflared:2022.4.0-amd64 tunnel login
```

Created tunnel TUNNEL1 with id tunnelid, copy tunnel id and keep somewhere.

```
docker run -it --rm -v /mnt/user/appdata/cloudflared:/home/nonroot/.cloudflared/ cloudflare/cloudflared:2022.4.0-amd64 tunnel create TUNNEL1
```

#### Edit Tunnel Json Config File

`nano /mnt/user/appdata/cloudflared/config.yml`


```
tunnel: tunnelid
credentials-file: /root/.cloudflared/tunnelid.json

ingress:
  - service: https://reverseproxyip:443
    originRequest:
      originServerName: example.com
```

files in the folder for this profile, if you run multiple tunnels you should change folder name for that profile instead of cloudflared.


```
/mnt/user/appdata/cloudflared# ls
tunnelid.json  cert.pem  config.yml
```

#### Redirect Cloudflare to Tunnel


redirect cname of your root domain from dns settings on dash.cloudflare.com

Format: *tunnelid.cfargotunnel.com*

#### Create Docker Compose and Run Tunnel on Docker

```
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
```

*note: replace all 'tunnelid' section in the form with your tunnel id which is generated in permission step*
