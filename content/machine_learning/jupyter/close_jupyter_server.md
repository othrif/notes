---
title: "Setting up machine learning libraries with GPU"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Switch between gcc8 and gcc9

For tensorflow and pytorch, you need `gcc8` to compile code which is not the system default. Do the following to use `gcc8`:

``` bash 
sudo apt -y install build-essential
sudo apt -y install gcc-8 g++-8 gcc-9 g++-9
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 8 --slave /usr/bin/g++ g++ /usr/bin/g++-8
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 9 --slave /usr/bin/g++ g++ /usr/bin/g++-9
# Every time you want to make a selection, run:
sudo update-alternatives --config gcc
# press number corresponding to your choice
```


```python

```
