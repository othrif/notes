---
title: "Subsetting Numpy arrays"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
###  Subset numpy arrays


```python
x = [4 , 9 , 6, 3, 1]
y = np.array(x)
y[1]
high = y > 5
y[high]
```




    array([9, 6])




```python
print(y[high])
```

    [9 6]


### Indexing similar between lists and Numpy arrays


```python
x = ["a", "b", "c"]
x[1]
```




    'b'




```python
np_x = np.array(x)
np_x[1]
```




    'b'



### Methods can be different


```python
x = [4 , 9 , 6, 3, 1]
x+x
```




    [4, 9, 6, 3, 1, 4, 9, 6, 3, 1]




```python
np.array(x)+np.array(x)
```




    array([ 8, 18, 12,  6,  2])




```python

```
