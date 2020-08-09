---
title: "k-Fold Cross Validation"
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
from sklearn.model_selection import cross_val_score
from sklearn.tree import DecisionTreeRegressor # regression
from sklearn.metrics import accuracy_score
from sklearn.metrics import mean_squared_error as MSE
```

### Load data


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

### Evaluate the 10-fold CV error


```python
# Set SEED for reproducibility
SEED = 1

# Instantiate a DecisionTreeRegressor dt
dt = DecisionTreeRegressor(max_depth=4, min_samples_leaf=0.26, random_state=SEED)

# Fit dt to the training set
dt.fit(X_train, y_train)

# Compute the array containing the 10-folds CV MSEs
MSE_CV_scores = - cross_val_score(dt, X_train, y_train, cv=10, 
                       scoring='neg_mean_squared_error',
                       n_jobs=-1)

# Compute the 10-folds CV RMSE
RMSE_CV = (MSE_CV_scores.mean())**(1/2)

# Print RMSE_CV
print('CV RMSE: {:.2f}'.format(RMSE_CV))
```

    CV RMSE: 5.04



```python
# Predict the labels of the training set
y_pred_train = dt.predict(X_train)

# Evaluate the training set RMSE of dt
RMSE_train = (MSE(y_train, y_pred_train))**(1/2)

# Print RMSE_train
print('Train RMSE: {:.2f}'.format(RMSE_train))
```

    Train RMSE: 5.11


Good! 
Notice how the training error is roughly equal to the 10-folds CV error you obtained.
