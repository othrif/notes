---
title: "Hyperparameter tunning for trees with GridSearch for Random Forest"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
- Hyperparameter tuning:
    - computationally expensive,
    - sometimes leads to very slight improvement,
- Weight the impact of tuning on the whole project.


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
from sklearn.model_selection import GridSearchCV
# Metrics
from sklearn.metrics import mean_squared_error as MSE
from sklearn.metrics import accuracy_score
from sklearn.metrics import roc_auc_score

# Models
from sklearn.ensemble import RandomForestRegressor

# Set seed for reproducibility
SEED=1
```

### Load data


```python
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

### Get all hyperparameters of dt


```python
# Instantiate dt
rf = RandomForestRegressor(random_state=SEED)
print(dt.get_params())
```

    {'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'gini', 'max_depth': None, 'max_features': None, 'max_leaf_nodes': None, 'min_impurity_decrease': 0.0, 'min_impurity_split': None, 'min_samples_leaf': 1, 'min_samples_split': 2, 'min_weight_fraction_leaf': 0.0, 'presort': 'deprecated', 'random_state': 1, 'splitter': 'best'}


### Define search grid


```python
# Define the dictionary 'params_rf'
params_rf = {'n_estimators': [100,350,500],
    'max_features': ['log2', 'auto', 'sqrt'],
    'min_samples_leaf': [2,10,30]
}
```

### Search for optimical forest

grid search is an exhaustive search process, it may take a lot time to train the model


```python
# Instantiate grid_rf
grid_rf = GridSearchCV(estimator=rf,
                       param_grid=params_rf,
                       scoring='neg_mean_squared_error',
                       cv=3,
                       verbose=1,
                       n_jobs=-1)

# Fit 'grid_dt' to the training data
grid_rf.fit(X_train, y_train)
```

    Fitting 3 folds for each of 27 candidates, totalling 81 fits


    [Parallel(n_jobs=-1)]: Using backend LokyBackend with 4 concurrent workers.
    [Parallel(n_jobs=-1)]: Done  42 tasks      | elapsed:   12.2s
    [Parallel(n_jobs=-1)]: Done  81 out of  81 | elapsed:   19.8s finished





    GridSearchCV(cv=3, error_score=nan,
                 estimator=RandomForestRegressor(bootstrap=True, ccp_alpha=0.0,
                                                 criterion='mse', max_depth=None,
                                                 max_features='auto',
                                                 max_leaf_nodes=None,
                                                 max_samples=None,
                                                 min_impurity_decrease=0.0,
                                                 min_impurity_split=None,
                                                 min_samples_leaf=1,
                                                 min_samples_split=2,
                                                 min_weight_fraction_leaf=0.0,
                                                 n_estimators=100, n_jobs=None,
                                                 oob_score=False, random_state=1,
                                                 verbose=0, warm_start=False),
                 iid='deprecated', n_jobs=-1,
                 param_grid={'max_features': ['log2', 'auto', 'sqrt'],
                             'min_samples_leaf': [2, 10, 30],
                             'n_estimators': [100, 350, 500]},
                 pre_dispatch='2*n_jobs', refit=True, return_train_score=False,
                 scoring='neg_mean_squared_error', verbose=1)



### Evaluate the optimical forest


```python
# Extract best hyperparameters from 'grid_rf'
best_hyperparams = grid_rf.best_params_
print('Best hyerparameters:\n', best_hyperparams)

# Extract the best estimator
best_model = grid_rf.best_estimator_

# Predict test set labels
y_pred = best_model.predict(X_test)

# Compute rmse_test
rmse_test = (MSE(y_test, y_pred))**(1/2)

# Print rmse_test
print('Test RMSE of best model: {:.3f}'.format(rmse_test)) 
```

    Best hyerparameters:
     {'max_features': 'auto', 'min_samples_leaf': 2, 'n_estimators': 100}
    Test RMSE of best model: 51.779

