---
title: "2D Numpy arrays"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
###  Subset numpy arrays


```python
baseball = [[180, 78.4],
            [215, 102.7],
            [210, 98.5],
            [188, 75.2]]
```


```python
np_baseball = np.array(baseball)
```


```python
print(baseball_np)
print(type(np_baseball))
print(np_baseball.shape)
```

    [[180.   78.4]
     [215.  102.7]
     [210.   98.5]
     [188.   75.2]]
    <class 'numpy.ndarray'>
    (4, 2)



```python
np_baseball[2][1]
```




    98.5




```python
np_baseball[2,1]
```




    98.5




```python
np_baseball[:,1]
```




    array([ 78.4, 102.7,  98.5,  75.2])



### 2D Arithmetic


```python
np_mat = np.array([[1, 2],
                   [3, 4],
                   [5, 6]])
np_mat * 2

```




    array([[ 2,  4],
           [ 6,  8],
           [10, 12]])




```python
np_mat + np.array([10, 10])
```




    array([[11, 12],
           [13, 14],
           [15, 16]])




```python
np_mat + np_mat
```




    array([[ 2,  4],
           [ 6,  8],
           [10, 12]])




```python

```
