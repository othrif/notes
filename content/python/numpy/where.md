---
title: "Find index of elment with where"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import numpy as np
v = np.array([1,0,  1, 2, 1, 1, 1, 2, 0, 0, 2])
np.where(v >= 2, 1, 0)
```




    array([0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1])


