+++
title = "stirling-pdf docker compose"
image = "/images/post/stirlingpdf.jpg"
author = "Sedat"
date = "2025-02-24T00:02:08Z"
description = "stirling-pdf stirling pdf"
categories = ["Docker"]
type = "post"

+++

Deploying Stirling-PDF using Docker Compose provides an efficient and scalable way to run this powerful, open-source PDF management tool. Stirling-PDF offers a wide range of PDF-related features, including merging, splitting, compressing, and converting documents, all accessible via a web-based interface. With Docker Compose, users can easily set up and manage the containerized application by defining the service in a docker-compose.yml file. This approach simplifies deployment by handling dependencies, networking, and persistent storage configurations. By running Stirling-PDF in a Docker environment, users benefit from easy updates, isolated execution, and the ability to integrate it seamlessly into self-hosted infrastructures like Nextcloud or other document management systems.

***

- [Click here for more information.](https://hub.docker.com/r/frooodle/s-pdf)

**Docker compose:**

```
version: '3.3'
services:
  stirling-pdf:
    container_name: Stirling-PDF
    image: frooodle/s-pdf:latest
    deploy:
      resources:
        limits:
          memory: 4G
    healthcheck:
      test: ["CMD-SHELL", "curl -f http://localhost:8080/api/v1/info/status | grep -q 'UP' && curl -fL http://localhost:8080/ | grep -qv 'Please sign in'"]
      interval: 5s
      timeout: 10s
      retries: 16
    ports:
      - "8080:8080"
    volumes:
      - /stirling/latest/data:/usr/share/tessdata:rw
      - /stirling/latest/config:/configs:rw
      - /stirling/latest/logs:/logs:rw
    environment:
      DOCKER_ENABLE_SECURITY: "false"
      SECURITY_ENABLELOGIN: "false"
      LANGS: "en_GB,en_US,ar_AR,de_DE,fr_FR,es_ES,zh_CN,zh_TW,ca_CA,it_IT,sv_SE,pl_PL,ro_RO,ko_KR,pt_BR,ru_RU,el_GR,hi_IN,hu_HU,tr_TR,id_ID"
      SYSTEM_DEFAULTLOCALE: en-US
      UI_APPNAME: Stirling-PDF
      UI_HOMEDESCRIPTION: Demo site for Stirling-PDF Latest
      UI_APPNAMENAVBAR: Stirling-PDF Latest
      SYSTEM_MAXFILESIZE: "100"
      METRICS_ENABLED: "true"
      SYSTEM_GOOGLEVISIBILITY: "true"
    restart: on-failure:5
```

***

- *Access to the ui:*
`http://<hostip>:8080/`
