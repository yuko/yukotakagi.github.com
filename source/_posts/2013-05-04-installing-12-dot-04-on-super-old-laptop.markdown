---
layout: post
title: "Notes on installing ubuntu 12.04"
date: 2013-05-04 18:25
comments: true
categories: ubuntu
---

On a crappy old laptop that I bought back in 2005 for $300-ish.

Installing 12.04 LTS went smoothly until when I rebooted the machine as the last step of installation. Then it hung, and stopped responding after spitting this error.
```
[ 48.753669] b43-phy0 ERROR: Firmware file "b43/ucode5.fw" not found
[ 48.753687] b43-phy0 ERROR: Firmware file "b43/ucode5.fw" not found
[ 48.753698] b43-phy0 ERROR: You must go to http://wireless.kernel.org/en/users/...devicefirmware and download the correct firmware for this driver version. Please carefully read all instructions on this site.
``` 
According to [this](http://wireless.kernel.org/en/users/Drivers/b43#Devicefirmware), apparently I'm missing the driver for the specific Broadcom wireless chip.
[Other people who have encountered the same issue](https://answers.launchpad.net/ubuntu/+source/gnome-nettool/+question/198083) solved it by running
```
sudo apt-get install
firmware-b43-installer
```
in Terminal, however, my laptop hung even before booting up. So I don't have an access to Terminal.

First, to solve the hanging issue this, I did the following.

1. When it hung, force reboot
1. grub screen shows up. Press 'e' so it enters edit mode.
1. Move cursor to the line that reads "vt.handoff=..."
1. Add "b43.blacklist=yes" to that line. Press F10 to save.

Referenced [here](http://ubuntuforums.org/showthread.php?t=1966655).
This way the machine at least boots up. Note that the wireless doesn't work because of the missing driver, so plug in LAN cable. Then run
```
sudo apt-get
install firmware-b43-installer
``` 

Problem solved. Woot!


