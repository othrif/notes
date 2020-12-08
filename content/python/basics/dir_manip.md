---
title: "Manipulation of directories and files"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Create dir if it does not exist


```python
import os
path='/tmp/test'
if not os.path.exists(path):
    os.mkdir(path)
```

### Do something if dir exists (alternative)


```python
import pathlib
data_dir = pathlib.Path('data/')
if not data_dir.exists():
    print('do something')
```

    do something


### Change directory


```python
os.chdir(path)
print(f'New location is: {os.getcwd()!r}')
```

    New location is: '/private/tmp/test'


### Create file in directory and list
Options available: `os.O_RDONLY, os.O_WRONLY, os.O_RDWR, os.O_CREAT, os.O_APPEND`


```python
fd = os.open('mytext.txt', os.O_RDONLY | os.O_CREAT) # open file
print(f'Intial file: {os.listdir(path)}') # list content of directory
os.rename('mytext.txt', "mytest_rename.txt")
print(f'Renamed file:{os.listdir(path)}')
os.close(fd) # close
```

    Intial file: ['mytext.txt']
    Renamed file:['mytest_rename.txt']


### Remove directory and all its content


```python
import shutil
if os.path.exists(path) and os.path.isdir(path):
    shutil.rmtree(path)
```
