---
title: "Decision tree with classification"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
predict whether a tumor is malignant or benign based on two features: the mean radius of the tumor (radius_mean) and its mean number of concave points (concave points_mean)

### Import modules


```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier # classification
from sklearn.metrics import accuracy_score
from sklearn.metrics import mean_squared_error as MSE
```

### Load data


```python
# read csv into df
wbc = pd.read_csv('wbc.csv')

# Get features of interest and target labels
X = wbc.loc[:,['radius_mean','concave points_mean']]
y = (wbc.loc[:, 'diagnosis']=='M').astype(int)

# Split dataset into 80% train, 20% test
X_train, X_test, y_train, y_test= train_test_split(X, y, 
                                                   test_size=0.2, 
                                                   stratify=y, 
                                                   random_state=1)
```


```python
# Instantiate a DecisionTreeClassifier 'dt' with a maximum depth of 6
dt = DecisionTreeClassifier(max_depth=10, random_state=1)

# Fit dt to the training set
dt.fit(X_train, y_train)

# Predict test set labels
y_pred = dt.predict(X_test)
print(y_pred[0:5])

# Compute test set accuracy  
acc = accuracy_score(y_test, y_pred)
print("Test set accuracy: {:.2f}".format(acc))

```

    [1 0 0 1 0]
    Test set accuracy: 0.92

