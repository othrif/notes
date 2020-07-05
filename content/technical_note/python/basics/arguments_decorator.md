---
title: "Pass arguments to decorators "
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Pass argument to decorator
You cannot pass arguments to decorator, since it is only supposed to take-in a function to be decorated as an argument. Instead, you created a function that returns a decorator. Then the `@` is applied to the decorator returned by the function with an argument. See below for an example:


```python
def run_n_times(n):
  """Define and return a decorator"""
  def decorator(func):
    def wrapper(*args, **kwargs):
      for i in range(n):
        func(*args, **kwargs)
    return wrapper
  return decorator
```


```python
@run_n_times(5)
def multiply(a,b):
    print(a*b)
```


```python
multiply(2,4)
```

    8
    8
    8
    8
    8

