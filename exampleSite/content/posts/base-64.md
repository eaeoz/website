+++
title = "Base 64 Code and Decode"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-11T05:00:00Z
description = "base64 code decode"
categories = ["technology"]
type = "post"

+++
```
echo "sedat" | base64 -w 0
xxxxxxxx

node1:~# echo c2VkYXQK | base64 -d
sedat
```