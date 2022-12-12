+++
title = "Apt Command Usage (Debian/Ubuntu)"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2022-11-11T05:00:00Z
description = "apt command"
categories = ["linux"]
type = "post"

+++
Apt is a command line package management utility for Ubuntu and Debian Linux. Apt is used to install, remove, update and upgrade Debian packages from command line in Ubuntu and Debian systems. Apt (Advanced package tool) overcomes the issues and bugs that were noticed in apt-get command. To use apt command user must have sudo privileges.

In this post, we will cover 15 apt command examples in Ubuntu / Debian Linux. Let’s dive into the examples.

#### 1) Update Package Information 

‘apt update’ 
this command is used to fetch latest package information from configured sources, here sources could repository over the internet or local repository.

$ sudo apt update

It is always recommended to run this command before installing or upgrading packages.

#### 2) List Packages

To list all the available packages including installed and upgradeable use apt list command.

$ sudo apt list

To list only the installed packages, run

$ sudo apt list --installed

To List only upgradeable packages, run

$ sudo apt list --upgradeable

#### 3) Installing New Package

To install a new package, use ‘apt install‘ command followed by package name, example is shown below:

$ sudo apt install nginx

Or

$ sudo apt install nginx -y

When we don’t pass ‘-y’ option in ‘apt install’ command then it will prompt you to confirm for its installation. But when we specify ‘-y’ then it is auto confirm and will install the packages.

Apt-Install-Command-Ubuntu

#### 4) Remove Package

To remove a package then use ‘apt remove’ command followed by the package name.

$ sudo apt remove nginx

To remove package and configuration files associated to package then use ‘apt purge’

$ sudo apt purge nginx

#### 5) Upgrade Package

To upgrade all the packages which are currently installed on your system then run ‘apt upgrade’ command.

$ sudo apt upgrade

To upgrade a specific installed package then use following command

$ sudo apt install snapd --only-upgrade

#### 6) Full System Upgrade

Always be careful while upgrading the whole system, as it might remove the installed packages and will install the updated packages. It is generally used when we want to update minor versions of Ubuntu / Debian systems. (like Ubuntu 20.04  to Ubuntu 20.04.4).

$ sudo apt full-upgrade

#### 7) Search Package

To search a package, run ‘apt  search‘ command followed by package name.

$ sudo apt search phpmyadmin

$ sudo apt search ^mysql-server

$ sudo apt search httpd*

#### 8) View Information About Package

To view the information about a package, run ‘apt show’ command followed by package name

$ sudo apt show nginx

apt-show-command-ubuntu

#### 9) Autoremove Packages

Autoremove option in apt command is used to remove the packages that were 

installed automatically to satisfy the dependencies and now no longer needed.

$ sudo apt auotremove

$ sudo apt --purge autoremove

#### 10) List Package Dependencies

To list package dependencies run ‘apt depends’ followed by package name

$ sudo apt depends phpmyadmin

To list package dependencies recursively then run ‘apt rdepends’ followed by package name

$ sudo apt rdepends docker

#### 11) Downloading Package without Installing

To download a package in the current working directory, run ‘apt download’ command followed by the package name.

$ sudo apt download phpmyadmin

apt-download-ubuntu

#### 12) Hold and Unhold Package

When a package is marked as hold then that package will not be upgraded till it is marked as unhold again.

Let’s assume we want to mark nginx as hold the run beneath command

$ sudo apt-mark hold nginx

nginx set on hold.

$

To mark nginx package as unhold, run

$ sudo apt-mark unhold nginx

Canceled hold on nginx.

$

#### 13) Clear Apt Cache

When we run apt command then it is cached in /var/cache/apt/archives, Cache comes into the picture whenever we re-install the package as apt command looks for package in cache first. So cleaning up apt cache will free up the disk space as it will remove packages from the folder ‘/var/cache/apt/archives/’.

$ sudo apt clean

To clean obsolete deb-packages then run

$ sudo apt autoclean

#### 14) Edit Sources (sources.list)

Apt command refers /etc/apt/sources.list for package repository url. Using ‘apt edit-sources’ command, sources.list file can be edited, example is shown below:

$ sudo apt edit-sources

Apt-Edit-Sources-Ubuntu-Linux

It will open sources.list file in vi editor, so edit the file and then save & exit the fille.

#### 15) History of apt command

Apt command history is stored under ‘/var/log/apt/history.log’ file. So, to view the history of apt command, use below cat command

$ cat /var/log/apt/history.log

Or

$ tail -n 30 /var/log/apt/history.log   // This will list only last 30 lines
That’s all from this post. I assume you have found it informative. Please do not hesitate to share your queries and feedback in below comments section.
