---
title: "Color grid with pcolormesh"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Using `pcolormesh`
Docs: https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.pcolormesh.html#matplotlib.pyplot.pcolormesh


```python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(19680801)
Z = np.random.rand(6, 10)   # 6 x 10
x = np.arange(-0.5, 10, 1)  # len = 11 => 10 values
y = np.arange(4.5, 11, 1)  # len = 7 => 6 values

fig, ax = plt.subplots()
psm = ax.pcolormesh(x, y, Z,cmap='hot')
fig.colorbar(psm, ax=ax)
plt.show()
```


![png](pcolormesh_2_0.png)

