---
title: "Video to gif"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Mov to gif
Particularly useful to animate screen records.
``` bash 
ffmpeg -i input.mov -pix_fmt rgb8 -r 10 output.gif && gifsicle -O3 output.gif -o output.gif
```




```python

```
