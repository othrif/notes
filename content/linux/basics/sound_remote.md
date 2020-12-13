---
title: "Playing sound from linux server in client MacOS"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to setup working locally with remote files"
type: technical_note
draft: false
---


There are two configurations that needs to setup:

### Client side - MacOS

* Install PulseAudio with brew: `brew install pulseaudio`
* Configure a listening daemon to receive the audio from the remote machine: 
``` bash 
pulseaudio --load=module-native-protocol-tcp --exit-idle-time=-1 --daemon
# alias: pulse
```
* PulseAudio will listen on port 4713, double check with `lsof -i -P | grep -i "listen"`
* Connect to server with Reverst Port Tunnel: `ssh -pXX -R 24713:localhost:4713 server`, where 24713 is arbitrary
* Copy the PulseAudio cookie to the server: 
``` bash 
scp ~/.config/pulse/cookie server:~/.config/pulse/cookie
```
** Alternatively, add a default configuration to authenticate based on IP: `load-module module-native-protocol-tcp auth-ip-acl=127.0.0.1;clien/port` in `/etc/pulse/default.pa`

#### Diagnose what devices available

``` bash 
pulseaudio --load=module-native-protocol-tcp --exit-idle-time=-1 --daemon
pacmd list-sources
```

### Server side - Linux

* Install PulseAudio: `apt-get install pulseaudio`
* PusleAudio send to the chosen port: `export PULSE_SERVER="tcp:localhost:24713"`
* Check that your client is listening: `pactl info`
* Test audio is working: `play file.wav`



### More help 
* https://medium.com/@cristianduguet/play-remote-audio-over-an-ssh-connection-with-a-mac-client-9b7135dfe129
* https://wiki.archlinux.org/index.php/PulseAudio/Examples



