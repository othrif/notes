---
title: "Membership test"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Pythonic way of checking


```python
def contains(haystack, needle):
    if needle not in haystack:
        raise ValueError('Needle not found')

contains([23, 42, 0xbadc0ffee], 'needle')
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-4-c0a79d64f7a4> in <module>
          3         raise ValueError('Needle not found')
          4 
    ----> 5 contains([23, 42, 0xbadc0ffee], 'needle')
    

    <ipython-input-4-c0a79d64f7a4> in contains(haystack, needle)
          1 def contains(haystack, needle):
          2     if needle not in haystack:
    ----> 3         raise ValueError('Needle not found')
          4 
          5 contains([23, 42, 0xbadc0ffee], 'needle')


    ValueError: Needle not found


### With a loop


```python
def contains(haystack, needle):
    for item in haystack:
        if item == needle:
            return
    raise ValueError('Needle not found')
contains([23, 42, 0xbadc0ffee], 'needle')
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-6-c605d648b237> in <module>
          4             return
          5     raise ValueError('Needle not found')
    ----> 6 contains([23, 42, 0xbadc0ffee], 'needle')
    

    <ipython-input-6-c605d648b237> in contains(haystack, needle)
          3         if item == needle:
          4             return
    ----> 5     raise ValueError('Needle not found')
          6 contains([23, 42, 0xbadc0ffee], 'needle')


    ValueError: Needle not found


### Use for loop with else branch
Little bit confusing though, so avoid


```python
def contains(haystack, needle):
    """
    Throw a ValueError if `needle` not
    in `haystack`.
    """
    for item in haystack:
        if item == needle:
            break
    else:
        # The `else` here is a
        # "completion clause" that runs
        # only if the loop ran to completion
        # without hitting a `break` statement.
        raise ValueError('Needle not found')
        
contains([23, 42, 0xbadc0ffee], 'needle')
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-5-0869a17c6175> in <module>
         14         raise ValueError('Needle not found')
         15 
    ---> 16 contains([23, 42, 0xbadc0ffee], 'needle')
    

    <ipython-input-5-0869a17c6175> in contains(haystack, needle)
         12         # only if the loop ran to completion
         13         # without hitting a `break` statement.
    ---> 14         raise ValueError('Needle not found')
         15 
         16 contains([23, 42, 0xbadc0ffee], 'needle')


    ValueError: Needle not found

