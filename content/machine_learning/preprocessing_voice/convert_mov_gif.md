---
title: "Convert mov to gif"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
# Convert video `.mov` to `.gif`

first, install `gifsicle`:
``` bash 
brew install gifsicle
```

Convert video recorded with quicktime to gif:
``` bash 
ffmpeg -i screen-recording.mov  -s 600x400 -pix_fmt rgb24 -r 10 -f gif - | gifsicle --optimize=3 --delay=3 > coolest.gif
```
