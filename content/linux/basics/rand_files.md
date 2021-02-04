---
title: "Choose random files from a file"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to find files using the Linux command line."
type: technical_note
draft: false
---

### In macos

``` bash 
brew install coreutils
gshuf -n N input > output
```

### In linux
``` bash 
shuf -n N input > output
```