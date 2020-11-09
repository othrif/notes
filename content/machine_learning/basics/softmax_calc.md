---
title: "Calculate softmax"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Calculate softmax


$\sigma(\vec{z})_i = \frac{e^{z_i}}{\sum_{j=1}^{K}e^{z_j}}$


```python
from math import exp
import numpy as np

z = [13, 9, 9]
np.round(np.exp(z)/sum(np.exp(z)),2)
```




    array([0.96, 0.02, 0.02])


