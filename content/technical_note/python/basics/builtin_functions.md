---
title: "Built-in functions"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### List of most widely used python built-in functions

#### `help` or `?<module>`
get help on any `__builtin__` module


```python
?help
```


    [0;31mSignature:[0m   [0mhelp[0m[0;34m([0m[0;34m*[0m[0margs[0m[0;34m,[0m [0;34m**[0m[0mkwds[0m[0;34m)[0m[0;34m[0m[0;34m[0m[0m
    [0;31mType:[0m        _Helper
    [0;31mString form:[0m Type help() for interactive help, or help(object) for help about object.
    [0;31mNamespace:[0m   Python builtin
    [0;31mFile:[0m        /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.7/lib/python3.7/_sitebuiltins.py
    [0;31mDocstring:[0m  
    Define the builtin 'help'.
    
    This is a wrapper around pydoc.help that provides a helpful message
    when 'help' is typed at the Python interactive prompt.
    
    Calling help() at the Python prompt starts an interactive help session.
    Calling help(thing) prints help for the python object 'thing'.




```python
help(help)
```

    Help on _Helper in module _sitebuiltins object:
    
    class _Helper(builtins.object)
     |  Define the builtin 'help'.
     |  
     |  This is a wrapper around pydoc.help that provides a helpful message
     |  when 'help' is typed at the Python interactive prompt.
     |  
     |  Calling help() at the Python prompt starts an interactive help session.
     |  Calling help(thing) prints help for the python object 'thing'.
     |  
     |  Methods defined here:
     |  
     |  __call__(self, *args, **kwds)
     |      Call self as a function.
     |  
     |  __repr__(self)
     |      Return repr(self).
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  __dict__
     |      dictionary for instance variables (if defined)
     |  
     |  __weakref__
     |      list of weak references to the object (if defined)
    


#### `round()`

#### `max()`

#### Other 


```python
def demofunc(a,b):
  """
//This function is to demonstrate a few built-in functions in Python
  """
  print("Begin")
  print(max(a,b))
  print(abs(a),abs(b))
  print(float(a),b)
  print(callable(a))
  print(hash(a),hash(b))
  print(len('ab'))
  print(type(a))
  for i in range(2,4): print(i)
```


```python
demofunc(3,4)
```

    Begin
    4
    3 4
    3.0 4
    False
    3 4
    2
    <class 'int'>
    2
    3



```python

```
