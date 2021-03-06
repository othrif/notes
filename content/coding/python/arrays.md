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
# Manipulate list
A = list(range(10))
print(f'len() of A: {len(A)}')
A.append(5)
print(f'append() to A: {A}')
A.remove(5)
print(f'remove() first occurence from A: {A}')
A.insert(1, 999)
print(f'insert() first occurence from A: {A}')
print(f'min() of A: {min(A)}')
print(f'max() of A: {max(A)}')
del A[1]
print(f'del element with index i of A: {A}')
del A[:4]
print(f'del a range of elements of A: {A}')
```

    len() of A: 10
    append() to A: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 5]
    remove() first occurence from A: [0, 1, 2, 3, 4, 6, 7, 8, 9, 5]
    insert() first occurence from A: [0, 999, 1, 2, 3, 4, 6, 7, 8, 9, 5]
    min() of A: 0
    max() of A: 999
    del element with index i of A: [0, 1, 2, 3, 4, 6, 7, 8, 9, 5]
    del a range of elements of A: [4, 6, 7, 8, 9, 5]


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


### Binary search for sorted list
* `bisect` module maintains a list in sorted order without having to sort the list after each insertion  


```python
# index where the element needs to be inserted in a sorted list 
import bisect
A = list(range(10))
print(A)
bisect.bisect(A, 6) # similar to bisect.bisect_right()
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]





    7




```python
# if element exist, return index of the left of it
print(A)
bisect.bisect_left(A, 6) # similar to bisect.bisect_right()
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]





    6




```python
# insert the element and not just the index
A = list(range(10))
print(A)
bisect.insort(A, 7) # same as bisect.insort_right()
print(A)
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    [0, 1, 2, 3, 4, 5, 6, 7, 7, 8, 9]


### Sorting  


```python
# reverse in-place
A = list(range(10))
A.reverse()
print(A)
```

    [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]



```python
# return an iterator
A = list(range(10))
for i in reversed(A): print(i, end=',')
```

    9,8,7,6,5,4,3,2,1,0,


```python
# sort in-place
A = [4,3,2,1,0]
A.sort()
print(A)
```

    [0, 1, 2, 3, 4]



```python
# returns a copy
A = [4,3,2,1,0]
sorted(A)
```




    [0, 1, 2, 3, 4]



### Slicing


```python
# note the range is [0,5)
A = list(range(10))
A[0:5]
```




    [7, 8]




```python
# from the back
A[-3:-1]
```




    [7, 8]




```python
# skip n=2
A[0:5:2] 
```




    [0, 2, 4]




```python
# reverse with [::-1]
A[::-1] 
```




    [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]




```python
# rotate a list
A[5:] + A[:5]
```




    [5, 6, 7, 8, 9, 0, 1, 2, 3, 4]



### List comprehension
`[<expression> for element in <iterator over sequence> <logical condition>]`


```python
[x**2 for x in range(6) if x%2==0]
```




    [0, 4, 16]




```python
# multiple levels
A = [1,2,3]
B = ['a', 'b']
[(x,y) for x in A for y in B]
```




    [(1, 'a'), (1, 'b'), (2, 'a'), (2, 'b'), (3, 'a'), (3, 'b')]




```python
# convert 2D to 1D
M = [['a', 'b', 'c'],['d', 'e']]
[x for row in M for x in row]
```




    ['a', 'b', 'c', 'd', 'e']




```python
# 2 level looping
M = [[1,2,3], [4,5,6]]
[[x**2 for x in row] for row in M]
```




    [[1, 4, 9], [16, 25, 36]]



### Useful tips
* Use of `next(iterator[, default])`


```python
# remove the leading zeros
res = [0,0,1,2,3,4]
res[next((i for i,x in enumerate(res) if x!=0)):]
```




    [1, 2, 3, 4]




```python
# what if they are all zeros
res = [0,0,0,0,0]
res[next((i for i,x in enumerate(res) if x!=0), len(res)):]
```




    []



* `for-else` statement: search through a list and process each item until a flag item is found and then stop processing


```python
# Loop until something is found
mylist=[1,2,3]
for i in mylist:
    if i == 5:
        break
    print(i)
else:
    raise ValueError("List argument missing terminal flag.")
```

    1
    2
    3



    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-1-9dbebae898f3> in <module>
          6     print(i)
          7 else:
    ----> 8     raise ValueError("List argument missing terminal flag.")
    

    ValueError: List argument missing terminal flag.


### `get() dict`
`dictionary.get(keyname, value)` returns the value of the item with the specified key and value if key does not exist


```python
car = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

x = car.get("price", 15000)

print(x)
```

    15000


### `any()` and `all()`
* `any()` sequence of OR operations on the provided iterables. Stops the execution as soon as the result is known.
* `all()` sequence of AND operations on the provided iterables. Stops the execution as soon as the result is known.


```python
# short circuits after second element
print (any([False, True, False, False]))  
```

    True



```python
# short circuits at the first element
print (all([False, True, True, False]))
```

    False


### Checking for duplicates


```python
def has_duplicates(block):
    return len(block) != len(set(block))
a=[1,2,3,1]
print(has_duplicates(a))
```

    True


### Filter + lambda vs. list comprehension
Time is very close between the two, thought list comprehension slighlty faster.


```python
import timeit
block=[1,0,3,1,0]
time1=timeit.timeit(str(list(filter(lambda x: x != 0, block))), number=100000000)
print(time1)
time2=timeit.timeit(str([x for x in block if x != 0]), number=100000000)
print(time2)
```

    3.8697273540000197
    3.6555018579999796


### Loop over sub-blocks of a matrix
Useful when doing convolutions


```python
# Example with 9x9 matrix and sub-block of 3x3
import math
M = [[0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 1, 2, 0, 0], [0, 0, 0, 0, 6, 0, 4, 0, 0], [0, 0, 0, 2, 0, 0, 0, 0, 5], [7, 0, 0, 0, 0, 0, 0, 0, 0], [0, 8, 3, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 3, 3, 0], [0, 0, 4, 0, 0, 0, 0, 0, 0]]
m = len(M)
n = int(math.sqrt(m))

# Original matrix
print('Original matrix:')
for i in range(m):
    for j in range(m):
        print(M[i][j], end=', ')
    print('')
print('---')
print('Sub-blocks of the matrix:')
for i in range(n):
    for j in range(n):
        for a in range(i*n, (i+1)*n):
            for b in range(j*n, (j+1)*n):
                print(M[a][b], end=',')
            print('')
        print('---')
```

    Original matrix:
    0, 0, 0, 0, 0, 0, 0, 0, 0, 
    0, 0, 0, 0, 0, 0, 0, 0, 0, 
    0, 0, 0, 0, 0, 1, 2, 0, 0, 
    0, 0, 0, 0, 6, 0, 4, 0, 0, 
    0, 0, 0, 2, 0, 0, 0, 0, 5, 
    7, 0, 0, 0, 0, 0, 0, 0, 0, 
    0, 8, 3, 0, 0, 0, 0, 0, 0, 
    0, 0, 0, 0, 0, 0, 3, 3, 0, 
    0, 0, 4, 0, 0, 0, 0, 0, 0, 
    ---
    Sub-blocks of the matrix:
    0,0,0,
    0,0,0,
    0,0,0,
    ---
    0,0,0,
    0,0,0,
    0,0,1,
    ---
    0,0,0,
    0,0,0,
    2,0,0,
    ---
    0,0,0,
    0,0,0,
    7,0,0,
    ---
    0,6,0,
    2,0,0,
    0,0,0,
    ---
    4,0,0,
    0,0,5,
    0,0,0,
    ---
    0,8,3,
    0,0,0,
    0,0,4,
    ---
    0,0,0,
    0,0,0,
    0,0,0,
    ---
    0,0,0,
    3,3,0,
    0,0,0,
    ---

