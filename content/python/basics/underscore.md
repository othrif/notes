---
title: "Usage of underscores"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
There are 5 usages of underscores (`_`) in python

### Single leading underscore `_var`

* `_var` is intended for internal use. `from M import *` doesn’t import objects whose names start with an underscore.

``` python
# m.py
external = "external"
_internal = "internal"

# main1.py - doesn't work
from m import *
print(external)
# external
print(_internal)
# NameError: name '_internal' is not defined

# main2.py - work
from m import external, _internal
print(external)
# external
print(_internal)
# internal

# main3.py - work
import m
print(m.external)
# external
print(m._internal)
# internal
```

* Single leading underscore is used a lot in classes. Programmers can create private variables and methods


```python
class Time:
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self._day = day

    def _is_even_number(self, x):
        return x % 2 == 0

time = Time(2020, 7, 10)
print(time.year, time.month, time._day)
print(time._is_even_number(10))
```

    2020 7 10
    True


### Visual seperator of digits


```python
amount = 1_000_000.1
print(amount)
```

    1000000.1


### Values we don't care about


```python
for _ in range(3):
  print("I don't care about index")
```

    I don't care about index
    I don't care about index
    I don't care about index



```python
year, *_, second = (2020, 7, 10, 12, 10, 59)
print(_) 
```

    [7, 10, 12, 10]


### Single Trailing Underscore `var_`

Only use to avoid conflicts with Python keywords. 


```python
import keyword
print(keyword.kwlist)
```

    ['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']



```python
global_=2
```

### Double Leading Underscore `__var`
`__var` will have a different name in the class where the python interpreter overwrites such identifiers in a class to avoid conflicts of names between the current class and its subclasses.


```python
class Time:
    def __init__(self, year, month):
        self.year = year
        self._month = month
        self.__day = 1

time = Time(2020, 7)
print(dir(time))
```

    ['_Time__day', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', '_month', 'year']



```python
print(time.__day)
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-11-6ce3ac535632> in <module>
    ----> 1 print(time.__day)
    

    AttributeError: 'Time' object has no attribute '__day'



```python
print(time._Time__day)
```

    1


### Double Leading and Trailing Underscore __var__

Magic methods like `__init__`, `__call__`, `__slots__`, can be overwritten 


```python
class Time:
    def __init__(self, year, month):
        self.year = year
        self._month = month
        self.__day = 1

    def __str__(self):
        return f"year: {self.year}, month: {self._month}, day: {self.__day}"
      
time = Time(2020,7)
print(time)
```

    year: 2020, month: 7, day: 1

