---
title: "Python 3 in MacOS"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Change python to point to python3 by default

``` bash 
ls -l /usr/local/bin/python*
ln -s -f /usr/local/bin/python3.7 /usr/local/bin/python
```

### Which Python version

``` bash 
python -V
```

### Install package
``` bash 
pip install SomePackage --upgrade
```

### Upgrade package
``` bash 
pip install SomePackage --upgrade
```

### Main packages used

``` bash 
pip install numpy
pip install scipy
pip install scikit-learn
pip install matplotlib
pip install pandas
pip install jupyter notebook
```


```python

```
