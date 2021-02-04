---
title: "Copy random file from subfolder to new subfolders"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to find files using the Linux command line."
type: technical_note
draft: false
---

### To be used when i want to copy one file from many subfolders in a source folder to local subfolders

``` bash 
for i in $(ls /source/of/folders); do pat="/source/of/folders/$i/"; cp $pat/$(ls $pat | shuf -n 1) $i/.; done
```

### If I want to copy the n first files from one subdirectory to another
``` bash 
find <source> -maxdepth 1 -type f | head -n <number of files to copy> | xargs -I{} cp "{}" <destination>
```