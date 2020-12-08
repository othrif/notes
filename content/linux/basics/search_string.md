---
title: "Search for a substring inside all files"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to find files using the Linux command line."
type: technical_note
draft: false
---

### Search recurisvely
``` bash 
grep -r "substring" .
```

### ignore case distinctions:
``` bash 
grep -ri "substring" .
```

### to only display filenames
``` bash 
grep -r -l "othrif" .
```