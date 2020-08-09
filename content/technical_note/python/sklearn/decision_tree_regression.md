---
title: "Decision tree with Regression"
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
from sklearn.tree import DecisionTreeRegressor # regression
from sklearn.metrics import accuracy_score
from sklearn.metrics import mean_squared_error as MSE
```

### Load data


```python
# read csv into df
wbc = pd.read_csv('auto.csv')
wbc_data = pd.get_dummies(wbc, columns=["origin"])
```


```python
# read csv into df
wbc = pd.read_csv('auto.csv')
wbc_data = pd.get_dummies(wbc, columns=["origin"])

# Get features of interest and target labels
X = wbc_data.iloc[:,1:]
y = wbc_data.iloc[:, 0]

# Split dataset into 80% train, 20% test
X_train, X_test, y_train, y_test= train_test_split(X, y, 
                                                   test_size=0.2,
                                                  random_state=1)
```

### Decision Tree regressor


```python
# Instantiate a DecisionTreeRegressor 'dt' with a maximum depth of 8
dt = DecisionTreeRegressor(max_depth=8,
                           min_samples_leaf=0.13)

# Fit dt to the training set
dt.fit(X_train, y_train)

# Predict test set labels
y_pred = dt.predict(X_test)

# Compute mse_dt
mse_dt = MSE(y_test, y_pred)

# Compute rmse_dt
rmse_dt = mse_dt**(1/2)

# Print rmse_dt
print("Test set RMSE of dt: {:.2f}".format(rmse_dt))
```

    Test set RMSE of dt: 4.27

