---
title: "Load, plot different classes"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Plot different classes


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Read data
s = 'https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data'
df = pd.read_csv(s,header=None,encoding='utf-8')

# Select X, y
X = df.iloc[:100, [0,2]].values
y = np.where(df.iloc[:100, 4].values == 'Iris-setosa', -1, 1)


# plot data
plt.scatter(X[:50, 0], X[:50, 1],
            color='red', marker='o', label='setosa')
plt.scatter(X[50:100, 0], X[50:100, 1],
            color='blue', marker='x', label='versicolor')


plt.xlabel('sepal length [cm]')
plt.ylabel('petal length [cm]')
plt.legend(loc='upper left')

plt.savefig('02_06.png', dpi=300)
plt.show()
```


    
![png](plot_iri_2_0.png)
    

