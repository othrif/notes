---
title: "Inspect module and get traceback"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Inspect method


```python
# import required modules
import inspect
  
def fun(a,b):
    # product of 
    # two numbers
    return a*b
  
# use getsource()
print(inspect.getsource(fun))
```

    def fun(a,b):
        # product of 
        # two numbers
        return a*b
    


### Class hierarchy


```python
# create classes
class A(object):
    pass
  
class B(A):
    pass
  
class C(B):
    pass
  
# not nested
print(inspect.getmro(C))  
```

    (<class '__main__.C'>, <class '__main__.B'>, <class '__main__.A'>, <class 'object'>)

