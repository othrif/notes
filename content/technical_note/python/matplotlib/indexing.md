---
title: "Array indexing"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import numpy as np
```

### Basics


```python
ary = np.array([1,2,3,4,5])
```


```python
ary[0]
```




    array([1, 2, 3])




```python
ary[:3] # equivalent to ary[0:3]
```




    array([1, 2, 3])




```python
ary2d = np.array([[1,2,3,3],[4,5,6,1],[2,52,36,1]])
```


```python
ary2d
```




    array([[ 1,  2,  3,  3],
           [ 4,  5,  6,  1],
           [ 2, 52, 36,  1]])




```python
ary2d[1,2]
```




    6




```python
ary2d[1]
```




    array([4, 5, 6])




```python
ary2d[0] # entire first row
```




    array([1, 2, 3])




```python
ary2d[:,0] # entire first column
```




    array([1, 4])




```python
ary2d[1:3,2:4] # bottom 2x2 
```




    array([[ 6,  1],
           [36,  1]])




```python
ary2d[:,:2] # first two columns
```




    array([[ 1,  2],
           [ 4,  5],
           [ 2, 52]])




```python

```
