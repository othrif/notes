---
title: "Find and count unique elements in array"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Find unique element in array


```python
import numpy as np
v = [1,0,  1, 2, 1, 1, 1, 2, 0, 0, 2]
np.unique(v)
```




    array([0, 1, 2])



### Count how many occurences


```python
np.bincount(v)
```




    array([3, 5, 3])


