---
title: "Spliting audio in CLI with ffmpeg"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Calculate the total time of all audio files at a location.

``` bash 
ffmpeg -ss START_TIME_IN_MS -t DURATION_IN_MS -i INPUT OUTPUT.mp4
```
