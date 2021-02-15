---
title: "Arrays"
date: 2021-02-04T00:00:00+00:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Definition

Arrays in python are of `list` type that is dynamically resized. The `tuple` is similar but immutable. 

### Basic operations


```python
A = list(range(10))
print(f'len() of A: {len(A)}')
A.append(5)
print(f'append() to A: {A}')
A.remove(5)
print(f'remove() first occurence from A: {A}')
A.insert(1, 999)
print(f'insert() first occurence from A: {A}')
```

    len() of A: 10
    append() to A: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 5]
    remove() first occurence from A: [0, 1, 2, 3, 4, 6, 7, 8, 9, 5]
    insert() first occurence from A: [0, 999, 1, 2, 3, 4, 6, 7, 8, 9, 5]


### Copy
3 types: 
* assignment copy(**=**): makes the two variables point to the one list in memory
* shallow copy ([:] OR **copy.copy()**): constructs a new compound object and then (to the extent possible) inserts references into it to the objects found in the original
* deep copy (**copy.deepcopy()**): constructs a new compound object and then, recursively, inserts copies into it of the objects found in the original. **Slower but changes will NOT be reflected on the original list**

*Difference between shallow and deep copying is only relevant for compound objects (e.g. a list of lists, or class instances).*    
Reference: https://medium.com/@thawsitt/assignment-vs-shallow-copy-vs-deep-copy-in-python-f70c2f0ebd86

![Types of copies in python](copy.png)


```python
# Assignment copy
colors = ['red', 'blue', 'green']
b = colors
b.append('white')
print(f'Copied/modified list: {b}')
print(f'Original list ALSO modified: {colors}')
```

    Copied/modified list: ['red', 'blue', 'green', 'white']
    Original list ALSO modified: ['red', 'blue', 'green', 'white']



```python
# Shallow copy
a = [[1, 2], [2, 4]]
b = a[:] ## shallow copy
b.append([3, 6])
print(f'Copied/modified list: {b}')
print(f'Original list NOT modified: {a}')
```

    Copied/modified list: [[1, 2], [2, 4], [3, 6]]
    Original list NOT modified: [[1, 2], [2, 4]]



```python
# Shallow copy compound object => referenced to the original elements
a = [[1, 2], [2, 4]]
b = a[:] #shallow copy
b[0].append(3)
print(f'Copied/modified list: {b}')
print(f'Original list ALSO modified: {a}')
# List b has its own pointer, but its elements do not
```

    Copied/modified list: [[1, 2, 3], [2, 4]]
    Original list ALSO modified: [[1, 2, 3], [2, 4]]



```python
# Deep copy, need copy module
import copy
a = [[1, 2], [2, 4]]
b = copy.deepcopy(a) ## deep copy
b[0].append(3) 
print(f'Copied/modified list: {b}')
print(f'Original list NOT modified: {a}')
```

    Copied/modified list: [[1, 2, 3], [2, 4]]
    Original list NOT modified: [[1, 2], [2, 4]]



```python

```
