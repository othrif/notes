---
title: "Searching"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Using `where`

Function call: `where(condition, [x, y])`

Return elements chosen from x or y depending on condition. Used with multidimensions


```python
import numpy as np

np.where([[True, False], [True, True]], 
         [[1, 2], [3, 4]],
         [[9, 8], [7, 6]])
```




    array([[1, 8],
           [3, 4]])


