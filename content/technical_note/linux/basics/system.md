---
title: "Linux system commands"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
type: technical_note
draft: false
---

Linux is a free and open source operating system. There are many variants of Linux out there. They are typically called Linux distribution. Suse, OpenSUSE, Debian, Ubuntu, CentOS, Arch, Fedora, RHEL, Scientific Linux (SLC), all are common Linux distribution names. Knowing your os version and name can be very useful for security patches.

### print Linux kernel version
`uname -r`   
or
`cat /proc/version`   

###  find os name and version in Linux
`cat /etc/os-release`

### query the system hostname and related settings
`hostnamectl`    

### gives LSB (Linux Standard Base) and distribution-specific information on the CLI
`lsb_release -a`    

