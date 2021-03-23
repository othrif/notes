---
title: "Copy, shallow copy, deep copy in Numpy"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import numpy as np
```

### Shallow copy


```python
x = np.array([1, 2, 3])
y = x
z = np.copy(x)
```


```python
x[0] = 10
print('y=', y)
print('z=', z)
```

    y= [10  2  3]
    z= [1 2 3]


### Deep copy
Shallow copy does not copy object elements within arrays


```python
a = np.array([1, 'm', [2, 3, 4]], dtype=object)
b = np.copy(a)
b[2][0] = 10
a
```




    array([1, 'm', list([10, 3, 4])], dtype=object)



Use `copy.deepcopy()`


```python
import copy
a = np.array([1, 'm', [2, 3, 4]], dtype=object)
c = copy.deepcopy(a)
c[2][0] = 10
c
```




    array([1, 'm', list([10, 3, 4])], dtype=object)




```python
a
```




    array([1, 'm', list([2, 3, 4])], dtype=object)


