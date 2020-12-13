---
title: "Working with remote files via ssh"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to setup working locally with remote files"
type: technical_note
draft: false
---


This describes the way I can arrange my work to edit files in my laptop and update them remotely to my server.
There are two ways to edit files:

# Using PyCharm:

Open `PyCharm Professional`, `New project>Pure python>Previously configured interpreter > Interpreter: Remote python > create`
Change configuration: `Tools > Deployment > Mappings > Deployment path`

# Using Sublime Text

### Edit file on a remote server locally

``` bash 
# setup sublime cli 
sudo ln -s /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl /usr/local/bin/subl
# ssh into your machine with
ssh -R 52698:localhost:52698 <username>@<remotehost>
```
Can also add it to `~/.ssh/config`
``` python 
host gangsterT
HostName <XX.YY.ZZ.UU>
User <username>
RemoteForward 52698 localhost:52698
Port <XX>
```

In the server, install `rmate` in the remote machine by executing these commands:
``` bash
sudo wget -O /usr/local/bin/rmate https://raw.github.com/aurora/rmate/master/rmate
sudo chmod a+x /usr/local/bin/rmate
```

Now, everytime you want to edit a file in your remote server, you just run
`rmate <file>`

### Sublime cli

Open a whole project:
``` bash 
subl <path/to/folder>
```

Open a file:
``` bash 
subl <path/to/file>
```