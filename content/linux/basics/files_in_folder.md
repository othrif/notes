---
title: "How many files in the folder?"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to setup working locally with remote files"
type: technical_note
draft: false
---

### Number of files in each folder
``` bash 
for i in `ls -d */`; do num=`ls $i | wc -l`; echo "$i: $num"; done
```