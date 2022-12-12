+++
title = "Cloudflare Dynamic DNS API Update with Docker"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2022-11-11T05:00:00Z
description = "cloudflare dynamic dns"
categories = ["docker", "network"]
type = "post"

+++
*copy api key from cloudflare dashboard and write your hostname*

```
version: '2'
services:
  cloudflare-ddns:
    image: oznu/cloudflare-ddns:latest
    restart: always
    environment:
      - API_KEY=xxxx
      - ZONE=example.com
      - PROXIED=true
      - PUID=998
      - PGID=100
```