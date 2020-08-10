---
title: "Ensemble learning with Stochastic Gradient Boosting"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Motivation:
- GB involves an exhaustive search procedure.
- Each CART is trained to find the best split points and features.
- May lead to CARTs using the same split points and maybe the same features.

Procedure:
- Each tree is trained on a random subset of rows of the training data.
- The sampled instances (40%-80% of the training set) are sampled without replacement.
- Features are sampled (without replacement) when choosing split points.
- Result: further ensemble diversity.
- Effect: adding further variance to the ensemble of trees.


### Import modules


```python
# Manipulation
import numpy as np
import pandas as pd
# Visualization
import seaborn as sns
import matplotlib.pyplot as plt
# Selection
from sklearn.model_selection import train_test_split
# Metrics
from sklearn.metrics import mean_squared_error as MSE
# Models
from sklearn.tree import DecisionTreeClassifier
# Ensemble
from sklearn.ensemble import GradientBoostingRegressor
```

### Load data


```python
# Set seed for reproducibility
SEED=1

# read csv into df
df = pd.read_csv('bikes.csv')

# Get features of interest and target labels
X = df.drop('cnt',axis=1)
y = df['cnt']

# Split dataset into 80% train, 20% test
X_train, X_test, y_train, y_test= train_test_split(X, y, 
                                                   test_size=0.2, 
                                                   random_state=SEED)
```

### Define the Stochastic Gradient Boosting regressor


```python
# Instantiate sgbr
sgbr = GradientBoostingRegressor(max_depth=4, 
            subsample=0.9,
            max_features=0.75,
            n_estimators=200,                                
            random_state=2)
```

### Train the SGB classifier


```python
# Fit sgbr to the training set
sgbr.fit(X_train, y_train)

# Predict test set labels
y_pred = sgbr.predict(X_test)
```

### Evaluate the SGB classifier


```python
# Compute MSE
mse_test = MSE(y_test, y_pred)

# Compute RMSE
rmse_test = mse_test ** (1/2)

# Print RMSE
print('Test set RMSE of sgb: {:.3f}'.format(rmse_test))
```

    Test set RMSE of sgb: 45.143

