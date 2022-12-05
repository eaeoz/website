+++
title = "Yum Command Usage (CentOS/RHEL)"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-16T05:00:00Z
description = "rhel centos yum"
categories = ["technology"]
type = "post"

+++
```
yum check-update	Display list of available package updates
yum update
yum update pkg1	Update all packages or update the pkg1 package
yum install pkg	Install a package
yum localinstall pkg.rpm	Install a package from a file named pkg.rpm
yum erase pkg	Remove a package
yum remove pkg	Same as above
yum autoremove	Free disk space by removing unwanted packages
yum reinstall pkg	Reinstall a package
yum downgrade pkg	Downgrade a package to an older version
yum check	Check rpm database for errors/problems
yum clean packages	Delete cached packages database
yum clean all	Delete out all packages and meta data from disk cache
yum list
yum list installed
yum list php
yum list available	List package names
yum deplist pkg1	Show dependencies for a pkg1
yum info pkg	Show info about a package
yum search pkg
yum search regex	Search package names
yum provides string
yum whatprovides string	List package that provides the given file or other info
yum history list	Show a list of all yum command history action such as install/update/erase
yum history info ID	Get info of yum action ID
yum history undo ID	Undo the yum command action from ID
yum history redor ID	Redot the yum command action from ID
yum grouplist	List package groups
yum groupinstall ‘Group Name’	Install all packages in the given group name
yum groupinfo ‘Group Name’	See packages in the given group name
yum groupremove ‘Group Name’	Remove/Delete all packages in the selected group
yum repolist	Show a list of all enabled repositories
yum repoinfo repoID	Show info about repoID
yum repo-pkgs repoID list	Show packages from repoID repo
yum repo-pkgs repoID install	Install all packages from repoID repo
yum repo-pkgs repoID remove	Erase all packages from repoID repo
yum repo-pkgs repoID reinstall	Reinstall all packages from repoID repo
yum help
yum help command

other command examples:

man yum	Show help about yum command or read yum command man page
nmtui
systemctl restart network
/etc/sysconfig/network-scripts/ifcfg-eth0
dnf install snapd
firewall-cmd --list-all
firewall-cmd --zone=public --permanent --add-port 25000/tcp

```