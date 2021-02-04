---
title: "Linux system info"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to setup working locally with remote files"
type: technical_note
draft: false
---

To find hadrware information about your linux system, few commmands report useful infromation. If several options are given, they perform similar functions.


### Linux/kernel information
``` bash 
cat /proc/version
```

### Linux version 
``` bash 
cat /etc/issue
# or
lsb_release -a
```


### CPU and processing units
``` bash 
lscpu
cat /proc/cpuinfo
```

### Disk space of file systems
``` bash 
pydf # pretty
df -H
```

### Check RAM
``` bash 
free -m
```

### List all hardware
``` bash 
hwinfo --short
sudo lshw -short
```

### List pci buses and devices connected to them
``` bash 
lspci
```