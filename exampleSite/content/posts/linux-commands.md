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
##### Find which application using the port:
`netstat -lpn | grep :80`
***
##### Delete all files and folders:
`rm -rf *`
***
##### Delete all files (including hidden files):
`rm -rf .*`
***
##### To remove three 0 end of string (13000 to 13):
`echo "13000" | rev | cut -c 4- | rev`
