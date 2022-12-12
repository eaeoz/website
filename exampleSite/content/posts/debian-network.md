+++
title = "Debian Network and DNS Settings"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2022-11-11T05:00:00Z
description = "debian network settings"
categories = ["linux"]
type = "post"

+++
`/etc/network$ nano interfaces`

```
# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
allow-hotplug eth0
auto eth0
iface eth0 inet static
  address 192.168.1.238
  netmask 255.255.255.0
  gateway 192.168.1.1
  dns-nameservers 1.1.1.1
```

`/etc/network# systemctl restart networking.service`


these parameters can be use


for domain set

 `dns-domain sweet.home`

for dhcp assign
 `iface enp0s5 inet dhcp`


for ubuntu dns conf

 `sudo nano /etc/resolv.conf`

```
nameserver 127.0.0.1
nameserver 1.1.1.1
```