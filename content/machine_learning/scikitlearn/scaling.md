---
title: "Feature scaling"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Standardize vs Normalize


```python
import numpy as np

ex = np.array([0, 1, 2, 3, 4, 5])

# standardize
print('standardized:', (ex - ex.mean()) / ex.std())

# normalize
print('normalized:', (ex - ex.min()) / (ex.max() - ex.min()))
```

    standardized: [-1.46385011 -0.87831007 -0.29277002  0.29277002  0.87831007  1.46385011]
    normalized: [0.  0.2 0.4 0.6 0.8 1. ]



```python
X_train = np.random.randn(200, 2)
X_test  = np.random.randn(200, 2)
```

### Standardize


```python
from sklearn.preprocessing import MinMaxScaler

mms = MinMaxScaler()
X_train_norm = mms.fit_transform(X_train)
X_test_norm = mms.transform(X_test)
```

### Normalize


```python
from sklearn.preprocessing import StandardScaler

stdsc = StandardScaler()
X_train_std = stdsc.fit_transform(X_train)
X_test_std = stdsc.transform(X_test)
```
