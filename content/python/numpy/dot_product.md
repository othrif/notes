---
title: "Dot product"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Calculate dot product


```python
import numpy as np
X = np.array([[1,2],[3,4],[5,6],[7,8],[9,10]])
Y = np.array([1,2,3,4,5])
np.dot(X.T,Y)
```




    array([ 95, 110])




```python
X.T.dot(Y)
```




    array([ 95, 110])


