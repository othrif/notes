---
title: "Strings"
date: 2021-02-04T00:00:00+00:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Definition

String type is **immutable**. Need to allocate new strings when slicing or concatenating. Try to write values from the back, instead of front. Reduce space complexity by using the string itself instead of brute force O(n) solutions.

### Basic operations


```python
t = 'My first string'
s = ' first '
print(f'in: {s in t}')
print(f'strip(): |{s}| -> |{s.strip()}|')
print(f'startswith(): {t.startswith("M")}')
print(f'endswith(): {t.endswith("ing")}')
print(f'STR.split(SEP): {t.split(" ")}')
print(f'SEP.join(LIST): {"/".join(["hey", "ho", "O"])}')
print(f'STR.lower(): {t.lower()}')
mystr = f'Testing this string: {t}'
print(mystr)
```

    in: True
    strip(): | first | -> |first|
    startswith(): True
    endswith(): True
    STR.split(SEP): ['My', 'first', 'string']
    SEP.join(LIST): hey/ho/O
    STR.lower(): my first string
    Testing this string: My first string



```python
# all methods related to string
dir(s)
```




    ['__add__',
     '__class__',
     '__contains__',
     '__delattr__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__getitem__',
     '__getnewargs__',
     '__gt__',
     '__hash__',
     '__init__',
     '__init_subclass__',
     '__iter__',
     '__le__',
     '__len__',
     '__lt__',
     '__mod__',
     '__mul__',
     '__ne__',
     '__new__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__rmod__',
     '__rmul__',
     '__setattr__',
     '__sizeof__',
     '__str__',
     '__subclasshook__',
     'capitalize',
     'casefold',
     'center',
     'count',
     'encode',
     'endswith',
     'expandtabs',
     'find',
     'format',
     'format_map',
     'index',
     'isalnum',
     'isalpha',
     'isascii',
     'isdecimal',
     'isdigit',
     'isidentifier',
     'islower',
     'isnumeric',
     'isprintable',
     'isspace',
     'istitle',
     'isupper',
     'join',
     'ljust',
     'lower',
     'lstrip',
     'maketrans',
     'partition',
     'replace',
     'rfind',
     'rindex',
     'rjust',
     'rpartition',
     'rsplit',
     'rstrip',
     'split',
     'splitlines',
     'startswith',
     'strip',
     'swapcase',
     'title',
     'translate',
     'upper',
     'zfill']



## Useful tips

### convert string to number in a given base


```python
from functools import reduce
from string import hexdigits
def num_to_int (num_as_string, base):
    return reduce(lambda x,c: x * base + hexdigits.index(c.lower()), num_as_string, 0)
num_to_int('613', 7)
```




    304


