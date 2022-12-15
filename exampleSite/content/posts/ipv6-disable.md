+++
title = "IPv6 Disable (Debian and Redhat)"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-16T05:00:00Z
description = "debian redhat ipv6 disable"
categories = ["linux"]
type = "post"

+++

#### Red Hat-based distributions

Here's how to disable IPv6 on Linux if you’re running a Red Hat-based system:

Open the terminal window.

Change to the root user.

-----

Type these commands: 

```
sysctl -w net.ipv6.conf.all.disable_ipv6=1
sysctl -w net.ipv6.conf.default.disable_ipv6=1
sysctl -w net.ipv6.conf.tun0.disable_ipv6=1
``` 

To re-enable IPv6, type these commands:

```
sysctl -w net.ipv6.conf.all.disable_ipv6=0
sysctl -w net.ipv6.conf.default.disable_ipv6=0
sysctl -w net.ipv6.conf.tun0.disable_ipv6=0
sysctl -p
```

#### Debian-based distributions

Here's how to disable IPv6 on Linux if you’re running a Debian-based machine.

Open the terminal window.

Type this command:

sudo nano /etc/sysctl.conf

Add the following at the bottom of the file:

```
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
net.ipv6.conf.tun0.disable_ipv6 = 1
``` 

Save and close the file.

Reboot your device.

To re-enable IPv6, remove the above lines from /etc/sysctl.conf and reboot your device.
