+++
title = "Arp Installation and Commands For Linux"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-16T05:00:00Z
description = "arp installation commands"
categories = ["linux"]
type = "post"

+++
#### Installation

 Debian

`apt-get install net-tools`

 Ubuntu

`apt-get install net-tools`

 Alpine

`apk add net-tools`

 Arch Linux

`pacman -S net-tools`

 Kali Linux

`apt-get install net-tools`

 CentOS

`yum install net-tools`

 Fedora

`dnf install net-tools`

 Raspbian

`apt-get install net-tools`

 Dockerfile

 `dockerfile.run/arp`

 Docker

`docker run cmd.cat/arp arp`

#### Commands

Show current arp table:

`arp -a`

Clear the entire cache:

`sudo arp -a -d`

Delete a specific entry:

`arp -d address`

Create an entry:

`arp -s address mac_address`
