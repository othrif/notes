---
title: "Convert video"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
# Convert video

Convert video from one format to another:

``` bash 
ffmpeg -i input.mov -vcodec h264 -acodec mp2 output.mp4
```

# Run diagnosis

Run the following diagnosis for either audio or video:

``` bash 
ffmpeg -i output.mp4
ffprobe ouptut.mp4

```
