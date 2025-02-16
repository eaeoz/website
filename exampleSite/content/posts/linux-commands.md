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

(shows user puid and pgid)
id admin

(show for all users)
id
or
cat /etc/passwd
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
##### Find which application using the port (ps, pgrep, kill, pkill, killall)
```
netstat -lpn | grep :80
netstat -tulpan | grep LISTEN
sudo ss -anp | grep 5060
sudo ss -tulpn | grep LISTEN
sudo lsof -i:22 ## see a specific port such as 22 ##
lsof +L1


(to kill process: kill -signal pid)
kill -9 <processnumber>
or
kill -KILL <processnumber>



ps aux | fzf | awk '{print $2}' | xargs kill
ps -aux
sudo ps -a
sudo ps -U vivek
ps -U tom
ps -aux | more
sudo ps -aux | less



Press q to exit from above Ubuntu Linux pagers. You can search for a particular Ubuntu Linux process using grep command:

ps aux | grep nginx
sudo ps aux | grep vim
sudo ps aux | grep chromium-browser
sudo ps -aux | egrep 'sshd|openvpn'



(pkill command)
If you wish to kill a process by name, try pkill command. The syntax is:
pkill processName
pkill vim
pkill firefox
pkill -9 emacs
sudo pkill -KILL php7-fpm

(killall command)
The killall command kills processes by name, as opposed to the selection by PID as done by kill command:
killall vim
killall -9 emacs

```
***
##### Ls command
```
shows how many files in the folder
ls -la | wc -l

(other ls command examples)
ls -sh 				           diplay only file size
ls -l --block-size=M 		 using block size
ls -lh				           display file size in kb
```
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
##### tum bos klasorleri siler
`sudo rm -d *`
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
##### List and sort file and folders by size (ncdu command)
```
ncdu -x

5.4 GiB [##########] /home
   3.6 GiB [######    ] /var
 949.5 MiB [#         ] /lib
 935.1 MiB [#         ] /usr
 130.7 MiB [          ] /boot
  14.0 MiB [          ] /sbin
  12.6 MiB [          ] /bin
   7.3 MiB [          ] /etc
  40.0 KiB [          ] /root
e  16.0 KiB [          ] /lost+found
```
***
##### Du ve df commands
```
df -h /
df -kh  ------> for view space usage

lists all fs
df -Th

du -xh --max-depth=1
du -hsx

lists all directories with sizes
du -h -d1 -a -x /

show all files sizes.
du -sh

Find out which filesystem runs out of space
df -h

sort all folders smallest down
du | sort -n -r

List Folder Size (Ascending)
du | sort -g

List Folder Size (Descending)
du | sort -rg

inside logs all files sorted by size with all info -lrth if you dont use -S listed latest file at the bottom , within -S listet highest size bottom
ls -lrth -S

sort by date up to down
ls -ltr

sort by date down to up
ls -lt

total size of sda drives.
df -Th | grep "/dev/sda"
/dev/sda5      ext4       59G   17G   40G  30% /
/dev/sda1      vfat      511M  4,0K  511M   1% /boot/efi

clean the space allocated %5-%7 for root user
tune2fs -m0 /dev/sda5
```
***
##### 7zip install for ubuntu
```
sudo apt-get install p7zip-full
```
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
##### Listes usb devices connected
`lsusb`
***
##### Showing disk usage as percentage for file system
`lsblk -f`
***
##### Show disk ids
`blkid`
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
##### System uptime
```
uptime

uptime --pretty
up 2 hours, 22 minutes

uptime --since
2023-01-17 16:46:42

cat /proc/uptime
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
##### Show all the services running
```
sudo service --status-all
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
##### Download file from url using curl
`curl http://192.168.10.2:1111/not.txt -O not.txt`
***
##### Grep and sed commands
```
grep parteculer file
grep -Irl 'STRING' dir

use column as seperator print users at the first word column
awk -F : '{print $1}' /etc/passwd

print the column includes Derek
awk '/Derek/ {print $5}' .bashrc

replace and print only
head .bashrc | sed 's/Derek/Derk/g'

write to file changes with replace
sed -i 's/Derek/Derk/g' .bashrc

print file only first line
sed -n '1p' .bashrc

print range of the file
sed -n '1,5p' .bashrc
```
***
##### How to control process priority using nice and renice command
```
The primary purpose of the nice command is to run a process/command at a lower or higher priority. Use the renice command to alter the nice value of one or more running Ubuntu Linux processes. The nice value can range from -20 to 19, with 19 being the lowest priority. Say, you want to compile software on a busy Ubuntu Linux server. You can set a very low priority, enter:
nice -n 13 cc -c *.c &

Set a very high priority for a kernel update. Before rebooting Ubuntu Linux server, run:

nice --10 wall <<end
System reboots in 5 minutes for Ubuntu Linux kernel update!
Save all your work!!!

-- Sysadmin
end


To change the priority of a running process, type the following:
renice {Priority} -p {PID}
renice {Priority} {PID}
pgrep vim
renice 10 69947
sudo renice -10 $(pgrep vim)
ps -l
F S   UID     PID    PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1000    1295    1294  0  80   0 -  2183 do_wai pts/0    00:00:00 bash
0 R  1000    1311    1295  0  80   0 -  2517 -      pts/0    00:00:00 ps

(for vim with ctrl+z send it to background)



(we check here priority and niceness column, 80 and 0. by default priority 80 if you do nothing, also 0 for nicsness.)

ps -l

F S   UID     PID    PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1000    1295    1294  0  80   0 -  2183 do_wai pts/0    00:00:00 bash
0 T  1000    1317    1295  0  80   0 -  5233 do_sig pts/0    00:00:00 vim
0 R  1000    1324    1295  0  80   0 -  2517 -      pts/0    00:00:00 ps


nice
0


20 lowest value for niceness priority process can have
-20 highest value for niceness priority process can have
niceness go down mean, more priority and nicness going up less priority process has
(sudo renice command is enable us to change priority of process running)





sudo renice -10 -p 1317
(output is : 1317 (process ID) old priority 0, new priority -10)



(we have 2 diffrences in vim, negtive higher mean increase our process priority, lower number higher prioriry, and higher mean lower priority)

ps -l
F S   UID     PID    PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1000    1295    1294  0  80   0 -  2183 do_wai pts/0    00:00:00 bash
0 T  1000    1317    1295  0  70 -10 -  5233 do_sig pts/0    00:00:00 vim
0 R  1000    1338    1295  0  80   0 -  2517 -      pts/0    00:00:00 ps





renice 5 -p 1317
1317 (process ID) old priority -10, new priority 5


ps -l
F S   UID     PID    PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1000    1295    1294  0  80   0 -  2183 do_wai pts/0    00:00:00 bash
0 T  1000    1317    1295  0  85   5 -  5233 do_sig pts/0    00:00:00 vim
0 R  1000    1340    1295  0  80   0 -  2517 -      pts/0    00:00:00 ps






renice -n 6 -p 1317
1317 (process ID) old priority 5, new priority 6



ps -l
F S   UID     PID    PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1000    1295    1294  0  80   0 -  2183 do_wai pts/0    00:00:00 bash
0 T  1000    1317    1295  0  86   6 -  5233 do_sig pts/0    00:00:00 vim
0 R  1000    1345    1295  0  80   0 -  2517 -      pts/0    00:00:00 ps






(now we have another vim process has diffrent priority and niceness)

nice -n 10 vim
(with ctrl+z send it to background)

ps -l
F S   UID     PID    PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1000    1295    1294  0  80   0 -  2183 do_wai pts/0    00:00:00 bash
0 T  1000    1317    1295  0  86   6 -  5233 do_sig pts/0    00:00:00 vim
0 T  1000    1349    1295  0  90  10 -  5233 do_sig pts/0    00:00:00 vim
0 R  1000    1350    1295  0  80   0 -  2517 -      pts/0    00:00:00 ps



(renice you can set priority without -n but using nice you can't)
nice 12 vim
nice: ‘12’: No such file or directory




nice -n 12 vim

ps -l
F S   UID     PID    PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1000    1295    1294  0  80   0 -  2183 do_wai pts/0    00:00:00 bash
0 T  1000    1317    1295  0  86   6 -  5233 do_sig pts/0    00:00:00 vim
0 T  1000    1349    1295  0  90  10 -  5233 do_sig pts/0    00:00:00 vim
0 T  1000    1353    1295  0  92  12 -  5233 do_sig pts/0    00:00:00 vim
0 R  1000    1355    1295  0  80   0 -  2517 -      pts/0    00:00:00 ps

```
***
##### Inxi tool for hardware information
```
installation
sudo apt install inxi



example usage
inxi -Faz
or
inxi -b



Display battery status

inxi -B
Battery:
ID-1: BATT charge: 44.3 Wh (85.2%) condition: 52.0/53.2 Wh (97.7%)



Display CPU info

inxi -C
CPU:
  Info: 8-core model: AMD Ryzen 7 PRO 5850U with Radeon Graphics bits: 64
	type: MT MCP cache: L2: 4 MiB
  Speed (MHz): avg: 400 min/max: 400/4507 cores: 1: 400 2: 400 3: 400
	4: 400 5: 400 6: 400 7: 400 8: 400 9: 400 10: 400 11: 400 12: 400 13: 400
	14: 400 15: 400 16: 400



Combine options

inxi -S
System:
  Host: pop-os Kernel: 5.19.0-76051900-generic x86_64 bits: 64
	Desktop: GNOME 42.3.1 Distro: Pop!_OS 22.04 LTS

inxi -Sv
  CPU: 8-core AMD Ryzen 7 PRO 5850U with Radeon Graphics (-MT MCP-)
  speed/min/max: 634/400/4507 MHz Kernel: 5.19.0-76051900-generic x86_64
  Up: 20m Mem: 3084.2/15318.5 MiB (20.1%) Storage: 953.87 GiB (7.9% used)
  Procs: 346 Shell: Bash inxi: 3.3.13




Check the weather

inxi -w
Weather:
  Report: temperature: 14 C (57 F) conditions: Clear sky
  Locale: Wellington, G2, NZL
	current time: Tue 30 Aug 2022 16:28:14 (Pacific/Auckland)
	Source: WeatherBit.io

inxi -W istanbul,turkey
Weather:   Report: temperature: 27.01 C (81 F) conditions: broken clouds
           Locale: current time: Tue 05 Sep 2023 12:52:13 PM +03 Source: OpenWeatherMap.org
```
***
##### String command
```
The strings command on Linux is used to extract printable character strings from binary/executable files. The command reads the specified file and identifies sequences of printable characters that are at least 4 characters long and are terminated by a null byte (ASCII code 0) or a newline (ASCII code 10).
The basic syntax of the command is as follows:
strings [OPTIONS] FILENAME
Here, OPTIONS are the various flags that can be used with the command and FILENAME is the name of the file to search for strings. Some commonly used options include:

-a or --all: This option tells the strings command to scan the entire file, including uninitialized and loaded sections.
-f: This option tells the strings command to list the name of the file before each string.
-n: This option tells the strings command to display only strings that are at least n characters long.
-o: This option tells the strings command to print the offset of each string within the file.

Here is an example of using the strings command to search for strings in the file "binaryfile":
$ strings binaryfile
This will display all the printable character strings found in the file.
Note that the strings command is often used in combination with other tools, such as grep, sed, or awk, to filter and process the extracted strings further.
```
***
##### Bat command
```
Installation:
sudo apt install bat


Read from stdin, determine the syntax automatically (note, highlighting will only work if the syntax can be determined from the first line of the file, usually through a shebang such as #!/bin/sh)
curl -s https://sh.rustup.rs | bat

Read from stdin, specify the language explicitly
yaml2json .travis.yml | json_pp | bat -l json

Show and highlight non-printable characters:
bat -A /etc/hosts


Use it as a cat replacement:

bat > note.md  # quickly create a new file
bat header.md content.md footer.md > document.md
bat -n main.rs  # show line numbers (only)
bat f - g  # output 'f', then stdin, then 'g'.


You can use bat as a previewer for fzf. To do this, use bats --color=always option to force colorized output. You can also use --line-range option to restrict the load times for long files:
fzf --preview 'bat --color=always --style=numbers --line-range=:500 {}'

bat can be combined with tail -f to continuously monitor a given file with syntax highlighting.
tail -f /var/log/pacman.log | bat --paging=never -l log



batgrep "Derek" .bashrc

dont show other lines before and after:
batgrep "Derek" -B 0 -A 0 .bashrc

With batgrep, bat can be used as the printer for ripgrep search results.
batgrep needle src/


batdiff file1 file2

You can combine bat with git diff to view lines around code changes with proper syntax highlighting:
batdiff() {
    git diff --name-only --relative --diff-filter=d |
```
***
##### Tr command usage
```
echo "Hello World" | tr [a-z] [A-Z]
HELLO WORLD

cat message.txt
Learn Linux TV has recently reached 300000 subscribers! Wow!

cat message.txt | tr [a-z] [A-Z]
LEARN LINUX TV HAS RECENTLY REACHED 300000 SUBSCRIBERS! WOW!

tr [a-z] [A-Z] < message.txt
LEARN LINUX TV HAS RECENTLY REACHED 300000 SUBSCRIBERS! WOW!

echo "Hello World" | tr -d [a-z]
H W

cat usernames.txt
jay@localhostt
sam@localhostt
jan@localhostt
rodney@localhost

cat usernames.txt | tr -s "t"
jay@localhost
sam@localhost
jan@localhost
rodney@localhost
ann@localhost

cat message.txt
Learn Linux TV has recently reached 300000 subscribers! Wow!
cat message.txt | tr [:lower:] [:upper:]
LEARN LINUX TV HAS RECENTLY REACHED 300000 SUBSCRIBERS! WOW!

cat message.txt | tr -d [:alpha:]
      300000 ! !

cat message.txt
Learn Linux TV has recently reached 300000 subscribers! Wow!

cat message.txt | tr "!" "."
Learn Linux TV has recently reached 300000 subscribers. Wow.
```
***
##### Pushd popd and dirs commands
```
pushd /usr/share
/usr/share ~

pushd /usr/share/icons
/usr/share/icons /usr/share ~

pushd /usr/share/themes
/usr/share/themes /usr/share/icons /usr/share ~





latest directory
pushd +0
/usr/share

(list changed like this)
/usr/share /usr/share/themes /usr/share/icons

pushd +1
/usr/share/themes /usr/share /usr/share/icons






(remove latest path)
popd
/usr/share /usr/share/icons





(you can add this way but youll be still in the same directory)
pushd -n /var/local
/usr/share /var/local /usr/share/icons






(you can remove which number you want to)
popd +0
/var/local /usr/share/icons




dirs

(list with numbers)
dirs -v

(clear the stack)
dirs -c
```
***
##### Application from source installation and uninstallation examples (debian based)
```
sudo apt-get update
$sudo apt-get install filezilla

sudo apt --fix-broken install



sudo apt-get remove rhythmbox -y
sudo apt-get purge totem totem-plugins

sudo apt-get remove --purge libreoffice*
sudo apt-get clean
sudo apt-get autoremove

sudo apt-get purge --auto-remove cheese
sudo apt-get clean
sudo apt-get autoremove
```
***
##### How to setup a network bridge on an Ubuntu server using Netplan
```
Commands:
 ls /etc/netplan
 sudo cp /etc/netplan/00-installer-config.yaml /etc/netplan/00-installer-config.yaml.bak
 sudo nano /etc/netplan/00-installer-config.yaml
 sudo netplan generate
 sudo netplan apply
 ip a | grep " br0:" -A 3


Sample Yaml File:
# This is the network config
network:
  version: 2
  renderer: networkd
  ethernets:
    ens18:
      dhcp4: false
  bridges:
    br0:
      interfaces: [ens18]
      addresses: [192.168.1.2/24]
      gateway4: 192.168.1.1
      mtu: 1500
      nameservers:
        addresses: [8.8.8.8]
      parameters:
        stp: true
        forward-delay: 4
      dhcp4: no
```
***
##### Enable permit root login for ssh service
```
sudo nano /etc/ssh/sshd_config
PermitRootlogin yes
sudo systemctl reload sshd
```
***
##### Disable and remove SSH server on Ubuntu
```
sudo systemctl stop ssh
sudo systemctl disable ssh
sudo apt-get remove opnessh-server
(if you want to remove client use this command next)
sudo apt-get remove opnessh-client
```
***
##### To change the password of a specific user
```
sudo passwd -d <username>
sudo passwd -e <username>


Replace <username> with the actual username of the user whose password you want to change.

The -d option is used to delete the user's password, effectively making it empty.

The -e option is used to expire the user's password, forcing them to change it upon their next login.

By running these two commands in succession, you will remove the user's existing password and then expire it, prompting the user to set a new password when they log in next.

Note that you need to have root privileges or use the sudo command to execute these commands.


sudo userdel test
sudo groupadd test
sudo useradd -m -g test test
sudo passwd -d -e test
su test
```
***
##### For monitoring all filesystem usage
```
sudo apt install filelight
sudo filelight /
```
***
##### To truncate file from filesystem before you delete
```
> filename
rm -rf filename
```
***
