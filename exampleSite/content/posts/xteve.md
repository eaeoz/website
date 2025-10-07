+++
title = "xteve docker compose"
image = "/images/post/xteve.jpg"
author = "Sedat"
date = "2025-02-24T00:02:03Z"
description = "xteve docker compose"
categories = ["Docker"]
type = "post"

+++

xTeVe, IPTV kullanıcıları için geliştirilmiş, EPG (Elektronik Program Rehberi) desteği sunan güçlü bir m3u proxy ve kanal yönetim aracıdır. Docker üzerinden çalıştırılabilen bu uygulama, IPTV yayınlarını Plex, Emby ve Jellyfin gibi medya sunucularına entegre etmek için kullanılır. Kullanıcılar, xTeVe ile kanal listelerini özelleştirebilir, belirli kanalları filtreleyebilir ve EPG verilerini düzenleyerek daha iyi bir izleme deneyimi sağlayabilir. Hafif yapısı ve web tabanlı yönetim paneli sayesinde kolayca yapılandırılabilir ve birden fazla cihazda stabil şekilde çalışabilir. Özellikle Docker konteyneri olarak kullanıldığında, hızlı kurulum ve güvenli bir çalışma ortamı sunarak IPTV sistemlerini daha verimli hale getirir.

***

- [Click here for more information.](https://github.com/xteve-project/xTeVe)

**Docker compose:**

```
version: "3"
services:
  xteve:
    image: alturismo/xteve
    container_name: xteve
    hostname: xteve
    restart: unless-stopped
    networks:
      - default
    ports:
      - "34400:34400"
      - "1901:1900" # 1900 used by Plex
    environment:
      TZ: Europe/Istanbul
    volumes:
      - ./config:/config:rw
      - /dev/shm:/tmp/xteve

networks:
  default:
    driver: bridge
```

***

- *Access to the ui:*
`http://<hostip>:34400/web/`
