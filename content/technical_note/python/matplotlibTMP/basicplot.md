---
title: "Test plotting"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import numpy as np
import matplotlib.pyplot as plt
```

### Line plot


```python
x = [1, 2, 3, 4,10]
y = [10, 15, 17, 20,30]
plt.plot(x,y)

plt.xlabel('x-label')
plt.ylabel('y-label')
plt.title('My Title')
plt.yticks([0,5,10,15,20,25,30,40],
          ['zero', 'five', 'ten', 'fifteen', 'twenty', 'twenty five', 'thirty', 'fourty'])

plt.show()
```


![png](basicplot_3_0.png)



```python

```
