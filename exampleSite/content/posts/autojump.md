+++
title = "Autojump (jump to recent folders easly on command line)"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-11T05:00:00Z
description = "autojump command installation"
categories = ["technology"]
type = "post"

+++
in the history you should be visited that directory to work j command

```
sudo apt install autojump
python3 --version
sudo ln -s /usr/bin/python3 /usr/bin/python

git clone https://github.com/wting/autojump.git
cd autojump/
./install.py

cd
nano .bashrc

[[ -s /usr/share/autojump/autojump.sh ]] && source /usr/share/autojump/autojump.sh

or

[[ -s /home/sedat/.autojump/etc/profile.d/autojump.sh ]] && source /home/sedat/.autojump/etc/profile.d/autojump.sh
```

for info:

`cat /usr/share/doc/autojump/README.Debian`

#### Autojump for Debian

To use autojump, you need to configure you shell to source

`/usr/share/autojump/autojump.sh` on startup.

If you use Bash, add the following line to your `~/.bashrc` (for non-login

interactive shells) and your `~/.bash_profile` (for login shells):

`. /usr/share/autojump/autojump.sh`

If you use Zsh, add the following line to your `~/.zshrc` (for all interactive shells):

`. /usr/share/autojump/autojump.sh`

More Info:

https://github.com/wting/autojump