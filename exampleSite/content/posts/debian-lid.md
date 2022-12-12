+++
title = "Debian Closing Lid Ignore"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2022-11-11T05:00:00Z
description = "debian close lid ignore"
categories = ["linux"]
type = "post"

+++
```
user$ sudo vi /etc/systemd/logind.conf

HandleLidSwitch=ignore        <---- Set both of these
HandleLidSwitchDocked=ignore  <---- to ignore lid events.

user$ sudo systemctl restart systemd-logind
```