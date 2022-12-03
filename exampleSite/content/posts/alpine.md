+++
title = "Akaunting docker-compose"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-09T05:00:00Z
description = "akunting docker"
categories = ["technology"]
type = "post"

+++
https://alpinelinux.org/downloads/

download standart x86_64


min 256 ram for installation

min 128 ram for running basic


boot and login with root - setup-alpine command

dhcp, sys, setting etc..

reboot and remove iso disk




Docker Installation

apk add nano

nano /etc/apk/repositories

add this line - http://dl-cdn.alpinelinux.org/alpine/latest-stable/community

apk update

apk add docker

rc-update add docker boot

service docker start

reboot



apk add docker-compose

apk add bash

apk add iproute2




if bash not running run these commands first
```
apk add --no-cache --upgrade grep
apk add --no-cache --upgrade coreutils
apk add curl
```

apk add lsblk













Installation
>> apk add networkmanager


NetworkManager comes with a command line interface and a curses-based interface, nmcli and nmtui respectively or you can use a additional gui interface:

plasma-nm for Plasma integration and applet - network-manager-applet for a GTK system tray applet

After installation start NetworkManager:

>> rc-service networkmanager start


Also your user needs to be in the plugdev group:

>> adduser <YourUsername> plugdev









list running services - rc-service --list

rc-service networking status
 * status: started

rc-service networkmanager status
 * status: started




for alpine linux disable ipv6 on all docker containers:
echo net.ipv6.conf.all.disable_ipv6=1 | tee -a /etc/sysctl.conf && sysctl -p
echo net.ipv6.conf.default.disable_ipv6=1 | tee -a /etc/sysctl.conf && sysctl -p
ifconfig | grep inet


permanently-enable-ipv4-forwardingalpine:
echo net.ipv4.ip_forward=1 | tee -a /etc/sysctl.conf && sysctl -p




How To View CPU Temperature On Alpine Linux

Viewing CPU Temperature On Alpine Linux

Let us search and find the correct package name and drivers for CPU sensors. We use the apk command as follows:

>> apk search sensors

Confirm that we are going to install the correct package in Alpine Linux:

>> apk info lm-sensors


Installation

Install the lm-sensors package using apk command

>> apk add lm-sensors lm-sensors-detect

Setup

We need to run the following sensors-detect to identify and generate a list of kernel modules for your hardware. I am using 

ThinkPad X140e with AMD A4-5000 APU with Radeon(TM) HD Graphics

>> sensors-detect

All you have to do is type the following command:

>> sensors

Summing up

You learned how to install, set up, and configure the lm-sensors package on Alpine Linux to view CPU fan speed, temperature, and other data. We can use the watch command to execute a program periodically, showing output fullscreen. For instance, we can watch sensors as follows:

>> watch sensors

>> watch -n 1 sensors








