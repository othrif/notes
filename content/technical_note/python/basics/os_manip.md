---
title: "File, dir handling with os module"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Preliminary


```python
import os
```

### Current location


```python
print(f'Current location is: {os.getcwd()!r}')
```

    Current location is: '/Users/othmanerifki/projects/website/othrif.hugo/content/technical_note/python/basics'


### Create dir if it does not exist


```python
path='/tmp/test'
if not os.path.exists(path):
    os.mkdir(path)
```

#### Check by going to the newly created area and outputing path


```python
os.chdir(path)
print(f'New location is: {os.getcwd()!r}')
```

    New location is: '/private/tmp/test'


### Open file
Options available: `os.O_RDONLY, os.O_WRONLY, os.O_RDWR, os.O_CREAT, os.O_APPEND`


```python
fd = os.open(path+'/mytext.txt', os.O_RDONLY | os.O_CREAT) # open file
print(f'Intial file: {os.listdir(path)}')
os.rename('mytext.txt', "mytest_rename.txt")
print(f'Renamed file:{os.listdir(path)}')
os.close(fd) # close
```

    Intial file: ['mytext.txt']
    Renamed file:['mytest_rename.txt']


### Remove commands
#### 1. Remove directory and all its content


```python
import shutil
if os.path.exists(path) and os.path.isdir(path):
    shutil.rmtree(path)
```

#### 2. Alternative approach


```python
from pathlib import Path
dirpath = Path(path)
if dirpath.exists() and dirpath.is_dir():
    shutil.rmtree(path)
```
