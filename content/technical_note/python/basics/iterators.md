---
title: "Iterables with itr() and next()"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Iterarble and iterator
an iterable is an object that can return an iterator, while an iterator is an object that keeps state and produces the next value when you call `next()` on it


```python
flash = ['jay garrick', 'barry allen', 'wally west', 'bart allen']

# Print each list item in flash using a for loop
for item in flash:
    print('for-loop:'+item)


# Create an iterator for flash: superhero
superhero = iter(flash)

# Print each item from the iterator
print('next-iter:'+next(superhero))
print('next-iter:'+next(superhero))
print('next-iter:'+next(superhero))
print('next-iter:'+next(superhero))
```

    for-loop:jay garrick
    for-loop:barry allen
    for-loop:wally west
    for-loop:bart allen
    next-iter:jay garrick
    next-iter:barry allen
    next-iter:wally west
    next-iter:bart allen


### Iterator with `range()`


```python
small_value = iter(range(3))

print('next-iter:'+str(next(small_value)))
print('next-iter:'+str(next(small_value)))
print('next-iter:'+str(next(small_value)))

for i in range(3):
    print('for-loop:'+str(i))


# Create an iterator for range(10 ** 100): googol
googol = iter(range(10 ** 100))

# Print the first 5 values from googol
print('googol:'+str(next(googol)))
print('googol:'+str(next(googol)))
print('googol:'+str(next(googol)))
print('googol:'+str(next(googol)))
print('googol:'+str(next(googol)))

```

    next-iter:0
    next-iter:1
    next-iter:2
    for-loop:0
    for-loop:1
    for-loop:2
    googol:0
    googol:1
    googol:2
    googol:3
    googol:4


###  Functions that take iterators and iterables as arguments


```python
values = range(10,21)
print(values)


values_list = list(values)
print(values_list)


values_sum = sum(values)
print(values_sum)

```

    range(10, 21)
    [10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
    165

