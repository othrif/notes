---
title: "Array construction routines"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Routines
Several exist here: https://numpy.org/doc/stable/reference/routines.array-creation.html?highlight=array%20creation%20routines    
Focus on the most used 


```python
import numpy as np
```

### `ones`, `zeros`, `eye`, `diag` 


```python
np.ones((3, 3))
```




    array([[1., 1., 1.],
           [1., 1., 1.],
           [1., 1., 1.]])




```python
np.zeros((3, 3))
```




    array([[0., 0., 0.],
           [0., 0., 0.],
           [0., 0., 0.]])




```python
np.eye(3)
```




    array([[1., 0., 0.],
           [0., 1., 0.],
           [0., 0., 1.]])




```python
np.diag((1,2,3))
```




    array([[1, 0, 0],
           [0, 2, 0],
           [0, 0, 3]])



### Numbers in range


```python
np.arange(3,13)
```




    array([ 3,  4,  5,  6,  7,  8,  9, 10, 11, 12])




```python
np.arange(5)
```




    array([0, 1, 2, 3, 4])




```python
np.arange(1,10,2)
```




    array([1, 3, 5, 7, 9])




```python
np.linspace(0, 5, 5)
```




    array([0.  , 1.25, 2.5 , 3.75, 5.  ])



### Work with generators `fromiter`


```python
generator_expression = (i for i in range(10) if i % 2)
```


```python
type(generator_expression)

```




    generator




```python
np.fromiter(generator_expression, dtype=int)
```




    array([1, 3, 5, 7, 9])




```python

```
