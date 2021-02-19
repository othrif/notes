---
title: "Check from CLI if Jupyter is running and kill it"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Check what is running and kill it

For tensorflow and pytorch, you need `gcc8` to compile code which is not the system default. Do the following to use `gcc8`:

``` bash 
jupyter notebook list
jupyter notebook stop 8888
```
