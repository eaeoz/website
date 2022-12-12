+++
title = "Connect to a WIFI from Linux terminal using nmcli command"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2022-11-11T05:00:00Z
description = "linux wireless nmcli"
categories = ["linux"]
type = "post"

+++
```
nmcli dev status
nmcli device wifi list
nmcli con up conn_profile
nmcli con down conn_profile
nmcli dev wifi connect somepass password somepass
```