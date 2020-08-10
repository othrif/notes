---
title: "Hyperparameter tunning for trees with GridSearch for Tree"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
- Problem: search for a set of optimal hyperparameters for a learning algorithm.
- Solution: find a set of optimal hyperparameters that results in an optimal model.
- Optimal model: yields an optimal score.
- Score: in sklearn defaults to accuracy (classication) and $R^2$ (regression).
- Cross validation is used to estimate the generalization performance.

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
from sklearn.tree import DecisionTreeClassifier
```

### Load data


```python
# Set seed for reproducibility
SEED=1

# read csv into df
df = pd.read_csv('liver/indian_liver_patient_preprocessed.csv')

# Get features of interest and target labels
X = df.iloc[:,:-1]
y = (df.iloc[:,-1]).astype(int)

# Split dataset into 80% train, 20% test
X_train, X_test, y_train, y_test= train_test_split(X, y, 
                                                   test_size=0.2, 
                                                   stratify=y, 
                                                   random_state=SEED)
```

### Evaluate performance of an untuned dt


```python
dt = DecisionTreeClassifier(random_state=SEED)
dt.fit(X_train, y_train)
y_pred_proba = dt.predict_proba(X_test)[:,1]
test_roc_auc = roc_auc_score(y_test, y_pred_proba)
print('Test set ROC AUC score: {:.3f}'.format(test_roc_auc))
```

    Test set ROC AUC score: 0.540


### Get all hyperparameters of dt


```python
# Instantiate dt
dt = DecisionTreeClassifier(random_state=SEED)
print(dt.get_params())
```

    {'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'gini', 'max_depth': None, 'max_features': None, 'max_leaf_nodes': None, 'min_impurity_decrease': 0.0, 'min_impurity_split': None, 'min_samples_leaf': 1, 'min_samples_split': 2, 'min_weight_fraction_leaf': 0.0, 'presort': 'deprecated', 'random_state': 1, 'splitter': 'best'}


### Define search grid


```python
# Define params_dt
params_dt = {'max_depth': [2,3,4],
    'min_samples_leaf': [0.12,0.14,0.16,0.18]
}
```

### Search for optimical tree

`GridSearchCV` with the `estimator` option becomes the new classifer, as if I have instantiated the estimator with the correct set of hyperparameters.


```python
# Instantiate grid_dt
grid_dt = GridSearchCV(estimator=dt,
                       param_grid=params_dt,
                       scoring='roc_auc',
                       cv=5,
                       n_jobs=-1)

# Fit 'grid_dt' to the training data
grid_dt.fit(X_train, y_train)

# Extract best hyperparameters from 'grid_dt'
best_hyperparams = grid_dt.best_params_
print('Best hyerparameters:\n', best_hyperparams)

# Extract best CV score from 'grid_dt'
best_CV_score = grid_dt.best_score_
print('Best CV accuracy: {:.3f}'.format(best_CV_score))

# Extract the best estimator
best_model = grid_dt.best_estimator_

# Predict the test set probabilities of the positive class
y_pred_proba = grid_dt.predict_proba(X_test)[:,1]

# Compute test_roc_auc
test_roc_auc = roc_auc_score(y_test, y_pred_proba)

# Print test_roc_auc
print('Test set ROC AUC score: {:.3f}'.format(test_roc_auc))
```

    Best hyerparameters:
     {'max_depth': 3, 'min_samples_leaf': 0.12}
    Best CV accuracy: 0.729
    Test set ROC AUC score: 0.610


### Evaluate the optimical tree


```python
dt = DecisionTreeClassifier(max_depth=3, min_samples_leaf=0.12, random_state=SEED)
dt.fit(X_train, y_train)
y_pred_proba = dt.predict_proba(X_test)[:,1]
test_roc_auc = roc_auc_score(y_test, y_pred_proba)
print('Test set ROC AUC score: {:.3f}'.format(test_roc_auc))
```

    Test set ROC AUC score: 0.610


Good improvement upon an untuned classification-tree would achieve a ROC AUC score of 0.54
