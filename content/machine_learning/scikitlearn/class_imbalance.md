---
title: "Resampling for class imbalance"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Basic pipeline


```python
import numpy as np
import pandas as pd
from sklearn.preprocessing import LabelEncoder
from sklearn.model_selection import train_test_split

df = pd.read_csv('https://archive.ics.uci.edu/ml/'
                 'machine-learning-databases'
                 '/breast-cancer-wisconsin/wdbc.data', header=None)

X = df.loc[:, 2:].values
y = df.loc[:, 1].values
le = LabelEncoder()
y = le.fit_transform(y)

X_train, X_test, y_train, y_test = \
    train_test_split(X, y, 
                     test_size=0.20,
                     stratify=y,
                     random_state=1)

```


```python
print('Prior to imbalance')
print(f'Class 0: {X[y == 0].shape[0]}')
print(f'Class 1: {X[y == 1].shape[0]}')
```

    Prior to imbalance
    Class 0: 357
    Class 1: 212


### Create imbalanced set


```python
X_imb = np.vstack((X[y == 0], X[y == 1][:40]))
y_imb = np.hstack((y[y == 0], y[y == 1][:40]))
print('After creating imbalance')
print(f'Class 0: {X_imb[y_imb == 0].shape[0]}')
print(f'Class 1: {X_imb[y_imb == 1].shape[0]}')
```

    After creating imbalance
    Class 0: 357
    Class 1: 40


### Upsample the minority class


```python
from sklearn.utils import resample

print('Number of class 1 examples before:', X_imb[y_imb == 1].shape[0])

X_upsampled, y_upsampled = resample(X_imb[y_imb == 1],
                                    y_imb[y_imb == 1],
                                    replace=True,
                                    n_samples=X_imb[y_imb == 0].shape[0],
                                    random_state=123)

print('Number of class 1 examples after:', X_upsampled.shape[0])
```

    Number of class 1 examples before: 40
    Number of class 1 examples after: 357

