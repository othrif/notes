---
title: "Boolean operators with Numpy"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
The operational operators like `<` and `>=` worked with Numpy arrays out of the box. Unfortunately, this is not true for the boolean operators and, or, and not   
To use these operators with Numpy, you will need `np.logical_and()`, `np.logical_or()` and `np.logical_not()`


```python
import numpy as np
my_house = np.array([18.0, 20.0, 10.75, 9.50])
your_house = np.array([14.0, 24.0, 14.25, 9.0])
```


```python
np.logical_or(my_house>18.5,my_house<10)
```


```python
print(np.logical_or(my_house<11,your_house<11))
```

    [False False  True  True]



```python

```
