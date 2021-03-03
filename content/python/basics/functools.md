---
title: "Functools:reduce()"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### `reduce()`

Function call: `functools.reduce(function, iterable[, initializer])`   

You’re doing a fold or reduction when you reduce a list of items to a single cumulative value:    
1-**Apply** a function (or callable) to the first two items in an iterable and generate a partial result.   
2-**Use** that partial result, together with the third item in the iterable, to generate another partial result.   
3-**Repeat** the process until the iterable is exhausted and then return a single cumulative value.   

#### Vanilla version


```python
from functools import reduce

def my_add(a, b):
    result = a + b
    print(f"{a} + {b} = {result}")
    return result

numbers = [0, 1, 2, 3, 4]

print('Start by adding first two elments')
reduce(my_add, numbers)

print('\nStart by adding initializer with first element')
reduce(my_add, numbers, 100)
```

    Start by adding first two elments
    0 + 1 = 1
    1 + 2 = 3
    3 + 3 = 6
    6 + 4 = 10
    
    Start by adding initializer with first element
    100 + 0 = 100
    100 + 1 = 101
    101 + 2 = 103
    103 + 3 = 106
    106 + 4 = 110





    110



#### using `lambda`


```python
import random
numbers=[random.randint(0,10) for i in range(10)]
print(f'Input: {numbers}')
# addition
print(f'Addition: {reduce(lambda a, b: a + b, numbers)}')
# multiplication
print(f'Multiplication: {reduce(lambda a, b: a * b, numbers)}')
# Finding minimum
print(f'Minimum: {reduce(lambda a, b: a if a < b else b, numbers)}')
# Finding maximum
print(f'Maximum: {reduce(lambda a, b: a if a > b else b, numbers)}')
print(f'Checking if all values are true: {reduce(lambda a, b: bool(a and b), [1, 0, 1, 1, 1])}')
print(f'Checking if any values are true: {reduce(lambda a, b: bool(a or b), [0, 0, 1, 1, 0])}')
```

    Input: [1, 1, 9, 7, 2, 4, 7, 3, 7, 4]
    Addition: 45
    Multiplication: 296352
    Minimum: 1
    Maximum: 9
    Checking if all values are true: False
    Checking if any values are true: True


### more advanced 


```python
from functools import reduce
from string import hexdigits

reduce(lambda x,c: x * 7 + hexdigits.index(c.lower()), ['6','1','3'], 0)
```




    304




```python
def my_func(x, c):
    result = x * 7 + hexdigits.index(c.lower())
    print(f'{x} * 7 + dec({c}) = {result}')
    return result
reduce(my_func, ['6','1','3'], 0)
```

    0 * 7 + dec(6) = 6
    6 * 7 + dec(1) = 43
    43 * 7 + dec(3) = 304





    304


