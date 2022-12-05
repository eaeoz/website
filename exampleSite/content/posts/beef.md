+++
title = "Beef Social Engineering"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-11T05:00:00Z
description = "beef social engineering"
categories = ["hacking"]
type = "post"

+++
`sudo apt install beef-xss`

```
* for installing application link on the top bar notification

social engineering > fake notification bar (chrome)

* for fake facebook popup window to steal password
social engineering > pretty theft

* shows pic on broser and if you click let you download exe and send popup
social engineering > clippy

* redirecting browser to specific pages immediately
browser > hooked domain > redirect browser

* redirecting browser to specified page immediately and keep the page link same.
browser > hooked domain > redirect browser (iframe)

* gets cookies
browser > hooked domain > get cookie

* show on the page specified message at the top left
browser > hooked domain > replace content (deface)

* creates alert window with specified message
browser > hooked domain > create alert dialog

* creates text box popup and letyou type and returns data which is typed from browser
browser > hooked domain > prompt dialog
```

##### Beef on Hyper-V

on powershell

```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```


To install the enhanced session mode, run the following command in a terminal inside the Kali OS

`kali-tweaks`

opens up a GUI dialog box

Select Virtulization → configure. Once the installation is complete reboot your Kali OS.

On your Hyper-V host make go to `Action → Hyper-V settings → Enhanced Session Mode Policy → Allow enhanced session mode.` Make sure the checkbox is ticked.

While keeping your VM in shutdown mode, reboot your host OS.

Once the host OS is up, start the guest Kali OS. Connect to it and you should be presented with a dialog box that allows you to go full screen.