---
title: "Random numbers"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
###  Generate between 0 and 1


```python
import numpy as np
np.random.rand()
```




    0.719150310154773



###  Generate either 0 and 1
This changes every time i run this code


```python
for i in range(5):
    print(np.random.randint(0,2)) # generate 0 or 1, not [0,2) upper boundary is exclusive
```

    0
    1
    0
    0
    0


### Reproducibility with `seed()`
Insure reproducibility of the resutls by setting a seed. The sequence of random generated will be the same, everytime you run your program. this is why this is a *pseudo random generator*


```python
np.random.seed(123)
for i in range(5):
    print(np.random.randint(0,2)) # generate 0 or 1

```

    0
    1
    0
    0
    0

