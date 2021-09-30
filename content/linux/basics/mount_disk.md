---
title: "Mount external hard drive"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to zip and unzip files using the Linux command line."
type: technical_note
draft: false
---

### Find drives in the system
``` bash
sudo fdisk -l
```
Main drive is `sda` and external drives are usually `sdb`. Find the partition with the largest size in my case `sdb4`

### Mount drive
``` bash
mkdir /mnt/usbdrive
sudo mount /dev/sdb4 /mnt/usbdrive
```

