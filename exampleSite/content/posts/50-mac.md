+++
title = "50 Mac Terminal Commands"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-07T05:00:00Z
description = "mac commands"
categories = ["technology"]
type = "post"

+++
-say

-security find-generic-password -wa "wifissidnametypehere"

-security find-generic-password -wa "wifissidnametypehere" | pbcopy

-command + option + shift + v (copy plain text)

-caffeinate (as long as terminal open coputer keep on and ctrl+c stop)

-command + shift + 3 (save screenshot) command +shift+4 (part of the 

-page rectiangle) command+ctrl+shift+4 (goes to your clipboard)

-defaults write com.apple.screencapture name "yessss"

-defaults write com.apple.screencapture type jpg ( example:jpg)

-default write com.apple.screencapture location ~/Desktop/screenshots

-passwd

-security set-keychain-password

-cd

-ls

-pwd

-whoami

-mv

-cp

-ditto (alternative to cp)

-df -h

-nano

-man

-open

-ping

-ifconfig

-grep

-awk ( ifconfig en0 | grep inet | awk '{ print $2 }' ) getting only ip 
address ipv4 and ipv6

-traceroute

-dig

-ps (ps -ax | grep thisascript, kill -9 processnumber)

-top (top -o rsize) most memory usage

-kill

-which $SHELL

-bash (terminal linux)

-zsh (terminal mac)

-uptime

-sudo killall -HUP mDNSResponder; sudo killall -HUP 

-mDNSResponderHelper; sudo dscacheutil -flushcache

-qlmanage -p ~/Desktop/filename (for quick view file)

-diff nick1 nick2 (compare 2 files diffrences)

-curl https://raw.githubusercontent.com/test/random/main/test_kjv > test.txt

-leave 1245 ( for setting alarm to leave terminal )

-history

-disable gatekeeper (sudo spctl --master-disable)

-brew /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

-cmatrix (brew install cmatrix)

-asciiquarium (brew install asciiquarium)

-toilet (brew install toilet) toilet Hi Sedat

-tetris (brew install samtay/tui/tetris

-python3, python3 -m http.server, ctrl+x to end web server for file share

-shutdown, shutdown -r now

-sudo touch id (sudo nano /etc/pam.d/sudo, and copy this to the first line:auth sufficient pam_tid.so) save click ok, then run and test with sample command: sudo killall -HUP mDNSResponder (clear dns cache)

use this command to see what you download
-sqlite3 ~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV* 'select LSQuarantineDataURLString from LSQuarantineEvent'

clear browsing history
-sqlite3 ~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV* 'delete from LSQuarantineEvent'














