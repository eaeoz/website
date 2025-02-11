+++
title = "Linux Commands"
image = "/images/post/linuxcommands.jpg"
author = "Sedat"
date = "2025-02-08T00:06:00Z"
description = "linux commands"
categories = ["Linux"]
type = "post"

+++
Linux shell commands provide powerful tools for managing files, processes, and system configurations efficiently. Basic commands like ls list directory contents, cd navigates between directories, and pwd shows the current working directory. File operations include cp for copying, mv for moving or renaming, and rm for deleting files. The cat command displays file contents, while grep helps search text within files. For process management, ps lists active processes, kill terminates a process, and top provides real-time system monitoring. The chmod and chown commands manage file permissions and ownership. Networking tools like ping test connectivity, and curl or wget fetch content from URLs. To execute commands with administrative privileges, sudo is used. With powerful scripting capabilities, Linux shell commands enable automation, troubleshooting, and efficient system administration.

***
##### To change hostname
```
sudo hostnamectl set-hostname new_hostname

or

sudo hostname new_hostname
cat /etc/hostname
```
***
##### Set timezone:
`sudo timedatectl set-timezone Turkey`
***
##### Set keyboard layout
```
dpkg-reconfigure keyboard-configuration
service keyboard-setup restart


if you cant find command dpkg-reconfigure:

apt-get install console-data
apt-get install console-setup
apt-get install console-locales
apt-get install keyboard-configuration

Do the dpkg-reconfigure for each of the packets above. REBOOT.
```
***
##### Find current user and directory
```
whoami
pwd
```
***
##### Find information about linux commands
```
man
(example)
man trash-cli

tldr
(example)
tldr trash-cli
(update)
tldr --update

Examples:

man (Manual Pages)

man ls – Show manual for the ls command.
man -k keyword – Search for a command by keyword.
man 5 passwd – View section 5 of the passwd manual.
man -f ls (or whatis ls) – Brief description of ls.
man -P cat ls – Show ls manual without pagination.

tldr (Simplified Man Pages)

tldr ls – Get a short summary of ls usage.
tldr --list – List all available tldr pages.
tldr -u – Update the local tldr cache.
tldr --random – Show a random tldr page.
tldr tar – Quickly check tar command examples.
```
***
##### Find which application using the port
```
netstat -lpn | grep :80

or

ss -anp | grep 5060

(to kill process)
kill -9 <processnumber>
ps aux | fzf | awk '{print $2}' | xargs kill

```
***
##### Shows how many files in the folder
`ls -la | wc -l`
***
##### To view live logs
`tail -f /var/log/asterisk/queue_log`
***
##### Delete all files and folders
`rm -rf *`
***
##### Delete all files (including hidden files)
`rm -rf .*`
***
##### To remove three 0 end of string (13000 to 13)
`echo "13000" | rev | cut -c 4- | rev`
***
##### Run command at diffrent directory
`(cd /var/log && cp -- *.log ~/Desktop)`
***
##### Speedtest using iperf3 tool
```
sudo apt update && sudo apt install -y iperf3


This command runs iperf3 in server mode, listening on port 5201.

iperf3 -s -p 5201


Replace <server-ip> with the actual IP address of the server. This will test network speed between the client and server on port 5201.

iperf3 -c <server-ip> -p 5201
```
***
##### Combined ip -c addr command
```
ip -c --brief addr show | awk '{print $1,$3}'

Output:
lo 127.0.0.1/8
ens18 192.168.10.3/29
docker0 172.17.0.1/16
```
##### Combined ip route command
```
ip route get 1 | sed -n 's/^.*src \([0-9.]*\) .*$/\1/p'

Output:
192.168.10.211
```
***
##### Check network activity
```
sudo apt install dstat
then
dstat --net --top-io-adv
-net/total- -------most-expensive-i/o-process-------
 recv  send|process              pid  read write cpu
   0     0 |chrome               1885   19k  17k0.4%

sudo apt-get install nethogs
sudo nethogs -v 3

sudo apt-get install iptraf -y
sudo iptraf
iptraf -i eth0
sudo iptraf -h

sudo iftop
sudo iftop -p
sudo iftop –I <interface_name>
sudo iftop -h

sudo nethogs
sudo nethogs <interface_name>
sudo nethogs –d 7
```
***
##### Delete existing active network connection (example: if you cant connect after vpn installation)
```
nmcli connection delete pvpn-ipv6leak-protection
nmcli connection show --active
```
***
##### Find display manager service path
`grep '/usr/s\?bin' /etc/systemd/system/display-manager.service`
***
##### Truncate all files in a directory
```
cd /<directory>/
find . -type f -exec sh -c '> $1' sh {} \;
```
***
##### List all users in a group
`getent group docker`
***
##### You can list currently logged-in users using these commands
```
(list all users)
id

w
w -h | wc -l
who
who | wc -l
last -a | head -n 10
```
***
##### Generate password example
```
openssl rand -base64 24

or

tr -dc A-Za-z0-9 </dev/urandom | head -c 30 ; echo ''

Output:
cQDGkh5oBRC86SaQcUDbXMq1YArCVC
```
***
##### Mount ntfs drive in linux at the startup
```
sudo blkid
lsblk
sudo apt-get install ntfs-3g
sudo nano /etc/fstab
UUID=68F8796FF8793BFE /jellyfin/drive ntfs-3g defaults 0 0
or (full permission 777)
UUID=68F8796FF8793BFE /shared ntfs-3g defaults,uid=1000,gid=1000,umask=000 0 0

sudo mount -a
(if you receive error reload daemon)
sudo systemctl daemon-reload
```
***
##### Install GRUB on all RAID BOOT partitions after first boot
`sudo dpkg-reconfigure grub-pc  -> check all drives you're after.`
***
##### Wget commands for different format and source
```
download folder from http source:
wget --recursive --no-parent https://xx.com/folder/subfolder
To avoid downloading the auto-generated index.html files, use the -R/--reject option:
wget -r -np -R "index.html*" http://example.com/configs/.vim/
download only pdf files:
wget --no-directories --content-disposition -e robots=off -A.pdf -r http://www.test.com/
```
***
##### Example symlink to root folder
`ln -s /var/lib/docker/volumes/<hash>/_data/data/user/files/Youtube/ /`
***
##### History output without numbering
```
history -w /dev/stdout

(or you can save to file)
history > history_for_print.txt
```
***
##### Alias command for .bashrc (when you type movie locate urself to specified folder)
`alias movie='cd /jellyfin/movie'`
***
##### Check which ports using by which protocol, app and pid
`netstat -lpn`
***
##### System uptime
```
uptime

uptime --pretty
up 2 hours, 22 minutes

uptime --since
2023-01-17 16:46:42
```
***
##### Cpu detailed info
`cat /proc/cpuinfo`
***
##### Find if your cpu support virtualization
```
egrep -c '(vmx|svm)' /proc/cpuinfo

(Find cpu vendor. If the output contains vmx then you have a Intel based processor and svm confirms that it is AMD processor. Flags		: fpu vme....)
egrep --color 'vmx|svm' /proc/cpuinfo
```
***
##### Load avarage
`cat /proc/loadavg`
***
##### Find applications using highest cpu usage:
`ps --sort pcpu | tail -5`
***
##### Active service logs
```
journalctl -xe

(for specific service example)
journalctl -xu docker.service
```
***
##### Give multiple files user permissions in a directory (example:asterisk)
```
chown -R asterisk.asterisk /var/lib/asterisk/sounds/en
find /var/lib/asterisk/sounds/en -type d -exec chmod 0775 {} \;
```
***
##### Add application (example:asterisk) to startup
`update-rc.d asterisk defaults`
***
##### Generate key in your windows machine if you don't have one
`ssh-keygen -t rsa -b 4096 -f $env:USERPROFILE\.ssh\id_rsa -N ""`
***
##### Add your public key to remote machine to access without password from windows
`type $env:USERPROFILE\.ssh\id_rsa.pub | ssh root@192.168.1.254 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"`
***
