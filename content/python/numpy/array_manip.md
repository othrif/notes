---
title: "Select array entries with another array"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Using `where()` and `take()`


```python
import numpy as np
y_pred = np.array([1,0,0,1,1,0,0])
y_true = np.array([1,0,1,1,1,1,0])
test_files = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
np.where(y_pred != y_true)
```




    (array([2, 5]),)




```python
np.take(test_files,np.where(y_pred != y_true)[0])
```




    array(['c', 'f'], dtype='<U1')


