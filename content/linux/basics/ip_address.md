---
title: "Setup port forwarding and ip addresses"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "Get my ip address"
type: technical_note
draft: false
---

# Find my ip addresses

### Check public ip address (same in MacOS and Linux):
``` bash
curl ifconfig.me
```

### Check ip address on MacOS

``` bash 
# Private address
ipconfig getifaddr en0
```


### Check ip address on Linux

``` bash 
hostname -I
```

# Setup ssh port forwarding

### Router
* Netgear: change ip address in http://routerlogin.net/
* AT&T: Add your device to allow portforwarding https://www.att.com/support/article/u-verse-high-speed-internet/KM1215101

### Configuration

* Add the host internal ip address to your router's port forwarding service
* Modify the default port in the host by accessing `/etc/ssh/sshd_config`
* Restart the ssh service with `sudo systemctl restart ssh`
* Some good tips here: https://dev.to/zduey/how-to-set-up-an-ssh-server-on-a-home-computer


