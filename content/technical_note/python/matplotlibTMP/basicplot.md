---
title: "Basic plotting"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Useful links:
- Gallery of example plots: https://matplotlib.org/3.1.1/gallery/index.html
- visualizing images: https://matplotlib.org/3.1.1/tutorials/introductory/images.html
- Animations: https://matplotlib.org/3.1.1/api/animation_api.html
- Geospatial data: https://scitools.org.uk/cartopy/docs/v0.15/matplotlib/intro.html
- Statistical visualization (Pandas + Matplotlib): https://seaborn.pydata.org/examples/index.html


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


![png](basicplot_4_0.png)



```python

```
