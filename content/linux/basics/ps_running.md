---
title: "Details about a process and time it was running"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to setup working locally with remote files"
type: technical_note
draft: false
---

### Details about a process
``` bash 
ps axfu 
ps -p <PID>
```

### How long it has been running
``` bash 
ps -p {PID-HERE} -o etime # H:M:S
ps -p {PID-HERE} -o etimes # seconds
```