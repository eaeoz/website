+++
title = "40 Windows Commands"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-07T05:00:00Z
description = "windows shortcut command"
categories = ["technology"]
type = "post"

+++
ipconfig
ipconfig /all

ipconfig /release
ipconfig /renew
ipconfig /displaydns | findstr Record
ipconfig /displaydns | findstr Record | clip
ipconfig /flushdns

nslookup
getmac /v
powercfg /energy
powercfg /batteryreport
assoc

chkdsk /f
chkdsk /r
sfc /scannnow

DISM /Online /Cleanup /CheckHealth
DISM /Online /Cleanup /ScanHealth
DISM /Online /Cleanup /RestoreHealth

tasklist
taskkill

netsh wlan show wlanreport
netsh interface show interface
netsh interface ip show address | findstr “IP Address”
netsh interface ip show dnsservers
netsh advfirewall set allprofiles state off
netsh advfirewall set allprofiles state on

ping -t
tracert -d
netstat -af
netstat -o
netstat -e -t 5
route print
route add
route add 192.168.40.0 mask 255.255.255.0 10.7.1.44
route delete 192.168.40.0
shutdown /r /fw /f /t 0


























