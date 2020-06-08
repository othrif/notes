---
title: "Sort by size of files/directories"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

### Human readable 
``` bash 
du -sh
```

### Sort by size
``` bash 
du -h -d 1 | sort -n -r
```
du -d 1 : Only the disk usage of the current level of directories and files is displayed    
sort -n -r : Sort in reverse order according to value