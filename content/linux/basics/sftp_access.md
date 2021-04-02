---
title: "Access and download files via sftp"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to setup working locally with remote files"
type: technical_note
draft: false
---

### Access server
``` bash 
sftp username@server
```

### Download from server
``` bash 
sftp username@server:./'my\ file.tar.gz .
```