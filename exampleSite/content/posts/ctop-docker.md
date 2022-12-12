+++
title = "Ctop Docker CLI"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2022-11-11T05:00:00Z
description = "ctop docker cli"
categories = ["docker"]
type = "post"

+++
```docker run --rm -ti \
  --name=ctop \
  --volume /var/run/docker.sock:/var/run/docker.sock:ro \
  quay.io/vektorlab/ctop:latest```