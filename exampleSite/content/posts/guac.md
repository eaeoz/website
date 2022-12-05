+++
title = "Apache Guacamole - (ssh and vnc remote desktop access on docker)"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-11T05:00:00Z
description = "apache guacamole ssh vnc rdp"
categories = ["docker"]
type = "post"

+++
```
docker run -d \
  -p 8082:8080 \
  -v /guacamole:/config \
  oznu/guacamole
```