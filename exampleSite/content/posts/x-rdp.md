+++
title = "Debian Xrdp Installation"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-16T05:00:00Z
description = "debian xrdp"
categories = ["linux"]
type = "post"

+++
```
sudo apt update
sudo apt upgrade
sudo apt install xfce4 xfce4-goodies xorg dbus-x11 x11-xserver-utils
sudo apt install xrdp
sudo systemctl status xrdp
sudo adduser xrdp ssl-cert
sudo systemctl restart xrdp
```

#### Configuring Xrdp

The Xrdp configuration files are stored in the /etc/xrdp directory. For basic Xrdp connections, you do not need to make any changes to the configuration files. Xrdp will use the default X Window desktop, which in this case, is XFCE.

The main configuration file is named xrdp.ini . This file is divided into sections and allows you to set global configuration settings such as security and listening addresses and create different xrdp login sessions.

Whenever you make any changes to the configuration file you need to restart the Xrdp service:

sudo systemctl restart xrdp

Xrdp uses startwm.sh file to launch the X session. To use another X Window desktop, edit this file.

#### Configuring Firewall

By default, Xrdp listens on port 3389 on all interfaces. If you run a firewall on your Debian server, which you should always do, you’ll need to add a rule that will enable traffic on the Xrdp port.

Assuming you use ufw to manage the firewall, run the following command to allow access to the Xrdp server from a specific IP address or IP range, in this example 192.168.1.0/24:

sudo ufw allow from 192.168.1.0/24 to any port 3389

If you want to allow access from anywhere (which is highly discouraged for security reasons) run:

sudo ufw allow 3389

If you are using nftables to filter connections to your system, open the necessary port by issuing the following command:

sudo nft add rule inet filter input tcp dport 3389 ct state new,established counter accept

For increased security, you may consider setting up Xrdp to listen only on localhost and creating an SSH tunnel that securely forwards traffic from your local machine on port 3389 to the server on the same port. Another secure option is to install OpenVPN and connect to the Xrdp server trough the private network.

#### Connecting to the Xrdp Server

Now that you have set up your Xrdp server, it is time to open your Xrdp client and connect to the server.

If you have a Windows PC, you can use the default RDP client. Type “remote” in the Windows search bar and click on “Remote Desktop Connection”. This will open up the RDP client. In the “Computer” field, enter the remote server IP address and click “Connect”.
