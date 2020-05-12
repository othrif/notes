---
title: "Broadcasting"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import numpy as np
```

### Broadcasting
Broadcast- ing allows us to perform vectorized operations between two arrays even if their dimensions do not match by creating implicit multidimensional grids

different dimensions:


```python
np.array([1,2,3])+1
```




    array([2, 3, 4])



same dimensions:


```python
ary1 = np.array([1,2,3])
ary2 = np.array([2,4,1])
ary1+ary2
```




    array([3, 6, 4])



different shapes:


```python
ary3 = np.array([[2,4,1],[1,2,3]])
ary1+ary3
```




    array([[3, 6, 4],
           [2, 4, 6]])



number of elements along the explicit axes and the implicit grid have to match:


```python
try:
    print(ary1 + np.array([2,3]))
except ValueError as e:
    print('ValueError:', e)
```

    ValueError: operands could not be broadcast together with shapes (3,) (2,) 


the 2-element array must have two elements along its first axis as well


```python
ary3 + np.array([[2], [3]])
```




    array([[4, 6, 3],
           [4, 5, 6]])




```python

```
