---
title: "Array math and universal functions"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import numpy as np
```

### Universal functions
NumPy provides vectorized wrappers for performing element-wise operations implicitly via `ufuncs` – short for universal functions   
`ufuncs` are implemented in compiled C code and very fast and efficient compared to vanilla Python    
Checkout more details here: https://numpy.org/doc/stable/reference/ufuncs.html?highlight=ufuncs

#### Binary ufuncs
`add`, `subtract`, `divide`, `multiply`   

Using list comprehension:


```python
lst = [[1,2,3],[4,5,6],[7,8,9]]
[[cell+1 for cell in row] for row in lst] 
```




    [[2, 3, 4], [5, 6, 7], [8, 9, 10]]



Using Numpy `add` ufunc


```python
lst = [[1,2,3],[4,5,6],[7,8,9]]
ary = np.array(lst)
ary = np.add(ary,1)
print(ary)
```

    [[ 2  3  4]
     [ 5  6  7]
     [ 8  9 10]]


Also uses operator overloading with math symbols: `+,-,/,*,**`


```python
ary = np.array(lst)
ary+1
```




    array([[ 2,  3,  4],
           [ 5,  6,  7],
           [ 8,  9, 10]])




```python
(ary+1)**2
```




    array([[  4,   9,  16],
           [ 25,  36,  49],
           [ 64,  81, 100]])



#### Unary ufuncs
Unary ufuncs: `log`, `log10`, `exp`, `sqrt`   
`reduce`: compute the sum or product of array element along a given axis. By default, axis=0 for rows.


```python
np.add.reduce(ary) # sum along rows
```




    array([12, 15, 18])




```python
np.add.reduce(ary,axis=1) # sum along columns
```




    array([ 6, 15, 24])



shorthands:  `add.reduce` = `sum`  



```python
ary.sum(axis=1)
```




    array([ 6, 15, 24])




```python
np.sum(ary, axis=1) # equivalent to ary.sum(...)
```




    array([ 6, 15, 24])




```python
ary.sum() # sum over all elements of the array
```




    45



##### Other unary ufuncs
- `mean`: computes the mean
- `std`: computes the standard deviation
- `var`: computes variance
- `np.sort`: sorts an array [docs](https://docs.scipy.org/doc/numpy/reference/generated/numpy.sort.html)
- `np.argsort`: returns indices that would sort an array
- `np.min`: returns the minimum value of an array
- `np.max`: returns the maximum value of an array
- `np.argmin`: returns the index of the minimum value
- `np.argmax`: returns the index of the maximum value
- `np.array_equal`: returns if the two arrays have the same shape and elements


```python
ary
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])




```python
ary.mean(axis=0) 
```




    array([4., 5., 6.])




```python
ary_std = ary.std(axis=1)
```


```python
ary_var = ary.var(axis=1) 
```


```python
np.array_equal(ary_std**2,ary_var)
```




    True




```python
ary=np.array([[3,11,8],[10,9,209]])
ary
```




    array([[  3,  11,   8],
           [ 10,   9, 209]])




```python
np.sort(ary) # sort along the last axis, i.e. columns
```




    array([[ 1,  3,  8],
           [ 2,  9, 10]])




```python
np.sort(ary,axis=1) # sort along the columns
```




    array([[ 1,  3,  8],
           [ 2,  9, 10]])




```python
np.sort(ary,axis=0) # sort along the rows
```




    array([[ 3,  1,  2],
           [10,  9,  8]])




```python
np.sort(ary,axis=None) # sort along flatened array 
```




    array([ 1,  2,  3,  8,  9, 10])




```python
np.argsort(ary,axis=0) # sort along the rows
```




    array([[0, 0, 1],
           [1, 1, 0]])




```python

np.min(ary,axis=1) # find min along columns
```




    array([3, 9])




```python
np.max(ary,axis=0) # find max along rows
```




    array([ 10,  11, 209])




```python
np.argmax(ary, axis=0)
```




    array([1, 0, 1])


