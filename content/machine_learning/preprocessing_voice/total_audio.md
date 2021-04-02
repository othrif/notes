---
title: "total time of audio"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Calculate the total time of all audio files at a location.

``` bash 
EPOCH='jan 1 1970'; sum=0; for i in `soxi * | grep Duration | awk -F" " '{print $3}' | grep :`; do sum="$(date -u -d "$EPOCH $i" +%s) + $sum"; done; echo "total = `echo $sum | bc` seconds"
```


```python

```
