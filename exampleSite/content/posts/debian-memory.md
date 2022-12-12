+++
title = "Debian Memory Usage Check"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2022-11-11T05:00:00Z
description = "debian memory usage check"
categories = ["linux"]
type = "post"

+++
#### Check Memory Usage

`ps -o pid,user,%mem,command ax | sort -b -k3 -r`

top

use k key and write pid to kill

```
PID: this column shows the process ID number.
USER: this column shows the user who runs the process.
PR: prioriory for running processes.
NI: nice value
VIRT: Virtual Memory (Swap) being used.
RES: Physical memory used.
SHR: Shared memory used.
S: Process status.
%CPU: amount of CPU used by the process.
%MEM: amount of RAM memory used by the process
TIME+: total time the process is running.
COMMAND: the program or command which executes the process.
```

Another way to check the memory usage is by reading the file /proc/meminfo, you can use the command less or open the location /proc/meminfo on a browser.
The file /proc/meminfo runs on memory and provides information on the memory use such as free, used, swap, buffers and shared memory.

`/# less /proc/meminfo`

The first command shows how to release memory from the cache, you can see the comparison of the free -m output before and after running the command:

`echo 3 > /proc/sys/vm/drop_caches`

nano /etc/sysctl.conf

To make it persistent you need to add the following line to /etc/sysctl.conf :

vm.swappiness=0

#### Testing Memory Hardware in Debian

This chapter shows how to analyze your ram memory for hardware issues.
The optimal way to test the ram memory is by booting the computer using the memtester feature instead of the OS granting Memtest greater access to the memory. When executed from the OS the effectivity decreases. To install memtester on the console run:

`/# apt install memtester`

To run memtest you should specify the memory size in kb and the number of times you want tests to run.

`/# memtester 16384 5`