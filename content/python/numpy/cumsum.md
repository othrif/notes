---
title: "Cumulative sum `cumsum`"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import matplotlib.pyplot as plt
import numpy as np
v = sorted(np.arange(0,10), reverse=True)
tot = sum(v)
plt.bar(range(0, 10), v/tot, alpha=0.5, align='center')
plt.step(range(0, 10), np.cumsum(v)/tot, where='mid')
plt.ylabel('Explained variance ratio')
plt.xlabel('Principal components')

plt.show()
```


![png](cumsum_1_0.png)

