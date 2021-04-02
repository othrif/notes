---
title: "Queues"
date: 2021-02-04T00:00:00+00:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
# Deque

Deques are a generalization of stacks and queues (the name is pronounced “deck” and is short for “double-ended queue”). Deques support thread-safe, memory efficient appends and pops from either side of the deque with approximately the same O(1) performance in either direction.

Call: `class collections.deque([iterable[, maxlen]])`

if `maxlen` is specifified, deque is bounded to the specified maximum length.

### Basic operations


```python
from collections import deque
d = deque('ghi')     
for elem in d:
    print(elem.upper())
```

    G
    H
    I



```python
d.append('j')  # append from tail
d.appendleft('f') # append from head
d
```




    deque(['f', 'g', 'h', 'i', 'j'])




```python
d.pop()                          # return and remove the rightmost item
```




    'j'




```python
d.popleft()                      # return and remove the leftmost item
```




    'f'




```python
list(d)                          # list the contents of the deque
```




    ['g', 'h', 'i']




```python
d[0]                             # peek at leftmost item
```




    'g'




```python
d[-1]                            # peek at rightmost item
```




    'i'




```python
list(reversed(d))                # list the contents of a deque in reverse
```




    ['i', 'h', 'g']




```python
d
```




    deque(['g', 'h', 'i'])




```python
d.rotate(1)                      # right rotation
d
```




    deque(['i', 'g', 'h'])




```python
d.rotate(-1)                     # left rotation
d
```




    deque(['g', 'h', 'i'])



### Recipes


```python
# Bounded length deques provide functionality similar to the tail filter in Unix
def tail(filename, n=10):
    'Return the last n lines of a file'
    with open(filename) as f:
        #print(f.readlines())
        return deque(f, n)
tail('./arrays.md')
```




    deque(['    ---\n',
           '    0,0,0,\n',
           '    0,0,0,\n',
           '    0,0,0,\n',
           '    ---\n',
           '    0,0,0,\n',
           '    3,3,0,\n',
           '    0,0,0,\n',
           '    ---\n',
           '\n'])




```python
# del d[n] implemented with rotate
def delete_nth(d, n):
    d.rotate(-n)
    d.popleft()
    d.rotate(n)

d = deque([0,1,2,3,4])
delete_nth(d, 2)
d
```




    deque([0, 1, 3, 4])


