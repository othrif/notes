---
title: "Jupyter kernel versions"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Version of python running


```python
import sys
print(sys.executable)
print(sys.version)
print(sys.path)
```

    /Users/othrif/.pyenv/versions/3.9.6/bin/python3.9
    3.9.6 (default, Jul 15 2021, 14:42:14) 
    [Clang 12.0.5 (clang-1205.0.22.9)]
    ['/Users/othrif/github/notes/content/python/basics', '/Users/othrif/.pyenv/versions/3.9.6/lib/python39.zip', '/Users/othrif/.pyenv/versions/3.9.6/lib/python3.9', '/Users/othrif/.pyenv/versions/3.9.6/lib/python3.9/lib-dynload', '', '/Users/othrif/.local/lib/python3.9/site-packages', '/Users/othrif/.pyenv/versions/3.9.6/lib/python3.9/site-packages', '/Users/othrif/.pyenv/versions/3.9.6/lib/python3.9/site-packages/IPython/extensions', '/Users/othrif/.ipython']


### List all kernels


```python
!jupyter kernelspec list
```

    Available kernels:
      python3.8    /Users/othrif/Library/Jupyter/kernels/python3.8
      python3.9    /Users/othrif/Library/Jupyter/kernels/python3.9
      python3      /Users/othrif/.pyenv/versions/3.9.6/share/jupyter/kernels/python3


### Install Jupyter kernels

``` bash 
python -m ipykernel install -name python3.9
```

You can also modify the `kernel.json` at `/usr/local/share/jupyter/kernels/python3.9/kernel.json` 
