+++
title = "hyper-v scripts and commands"
image = "/images/post/hyperv.jpg"
author = "Sedat"
date = "2025-02-08T00:04:00Z"
description = "hyperv scripts commands"
categories = ["Windows"]
type = "post"

+++
A Hyper-V batch script allows users to automate virtual machine management on Windows, streamlining tasks such as starting, stopping, creating, or configuring VMs without manually using the Hyper-V Manager. Useful commands like PowerShell.exe -Command "Start-VM -Name <VMName>" can start a VM, while Stop-VM and Checkpoint-VM help manage its state efficiently. Batch scripts can also automate network configurations, snapshots, and resource allocations, making them ideal for IT professionals and developers managing multiple virtual machines. By integrating these scripts into a scheduled task, users can ensure automatic VM management without manual intervention.

***

### Start VM

```
Start-VM -Name examplevm
```
***

### Start Multiple VM

```
$VMs = "k8s1", "k8s2", "k8s3"  # Replace with the names of your virtual machines

foreach ($VM in $VMs) {
    Start-VM -Name $VM
}
```

***

### Send Command to Remote SSH Client (Stop Remote Linux Machine)

```
$vmName = "examplevm"   # Replace with your actual Hyper-V VM name
$hostIP = "192.168.1.254"  # Replace with your VM's SSH IP address
$username = "root"

$vmState = (Get-VM -Name $vmName).State
if ($vmState -eq "Running") {
    Write-Output "Sending shutdown command to $vmName..."
    ssh -o StrictHostKeyChecking=no $username@$hostIP "poweroff"
    Write-Output "Shutdown command sent."
} else {
    Write-Output "$vmName is not running."
}
```
