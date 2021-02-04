---
title: "MacOS tricks"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Convert HEIC images to jpg or other formats
``` bash
# install imagemagick
brew install imagemagick

# convert a single image
magick convert foo.HEIC foo.jpg

# bulk convert multiple images
magick mogrify -monitor -format jpg *.HEIC
```
