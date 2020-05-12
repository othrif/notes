---
title: "Numpy syntax"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### NumPy array data structure
Python interface for working with multi-dimensional array data structures efficiently   
NumPy array data structure is called `ndarray`, which is short for n-dimensional array   


### Advantage
NumPy arrays use contiguous blocks of memory that can be efficiently cached by the CPU. While Python lists are arrays of pointers to objects in random locations in memory, leading to a more expensive memory-look-up.

### Disadvantage
NumPy arrays have a fixed size and are homogenous, which means that all elements must have the same type   
Adding and removing elements from the end of a Python list is very efficient, altering the size of a NumPy array is very expensive since it requires creating a new array and carrying over the contents of the old array 


### N-dimenstional Arrays
NumPy arrays can have up to 32 dimensions   


```python
import numpy as np
```

#### `array` function
Create a NumPy array from a list of lists   


```python
lstint = [[1,2,3],
      [4,5,6]]
```


```python
ary2dint = np.array(lstint)
ary2dint
```




    array([[1, 2, 3],
           [4, 5, 6]])



#### Data type function `dtype`
All data types defined here: https://numpy.org/doc/stable/user/basics.types.html   


```python
ary2dint.dtype
```




    dtype('int64')



Numpy array sees what type will work for all elements of the list before creating it 

 


```python
lstfloat = [[1,2.3,3],
      [4,5,6]]
```


```python
ary2df = np.array(lstfloat)
```


```python
ary2df.dtype
```




    dtype('float64')



### Cast array type with `astype`


```python
ary2dint.dtype
```




    dtype('int64')




```python
ary2dintTOfloat = ary2dint.astype(np.float)
```


```python
ary2dintTOfloat.dtype
```




    dtype('float64')



#### Size in byte with `itemsize`
Returns size of each element in the array (remember that ndarrays are homogeneous)


```python
ary2dintTOfloat.itemsize
```




    8



each element takes up 8 bytes * 8 bits/byte = 64 bits in memory

#### Size of array with `size`


```python
ary2dintTOfloat.size
```




    6



#### Dimension of array with `ndim`
number of dimensions of an array, similar to a rank of a tensor


```python
ary2dintTOfloat.ndim
```




    2



#### Elements of each dim with `shape`
number of elements along each array dimension (in the context of NumPy arrays, we may also refer to them as axes)   
Returns a tuple `()`.


```python
ary_shape = ary2dintTOfloat.shape
```


```python
type(ary_shape)
```




    tuple




```python
np.array([1, 2, 3]).shape
```




    (3,)




```python

```


```python
scalar = np.array(5)
scalar
```




    array(5)


