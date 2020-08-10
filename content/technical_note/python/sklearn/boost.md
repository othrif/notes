---
title: "Ensemble learning with AdaBoost"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
- Boosting: Ensemble method combining several weak learners to form a strong learner.
- Weak learner: Model doing slightly better than random guessing.
- Example of weak learner: Decision stump (CART whose maximum depth is 1).


- Train an ensemble of predictors sequentially.
- Each predictor tries to correct its predecessor.

- AdaBoost: Stands for Adaptive Boosting.
- Each predictor pays more attention to the instances wrongly predicted by its predecessor.
- Achieved by changing the weights of training instances.
- Each predictor is assigned a coefcient α.
- α depends on the predictor's training error.



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
from sklearn.metrics import roc_auc_score
# Models
from sklearn.tree import DecisionTreeClassifier
# Ensemble
from sklearn.ensemble import AdaBoostClassifier
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

### Define the AdaBoost classifier


```python
# Instantiate dt
dt = DecisionTreeClassifier(max_depth=2, random_state=1)

# Instantiate ada
ada = AdaBoostClassifier(base_estimator=dt, n_estimators=180, random_state=1)
```

### Train the AdaBoost classifier


```python
# Fit ada to the training set
ada.fit(X_train, y_train)

# Compute the probabilities of obtaining the positive class
y_pred_proba = ada.predict_proba(X_test)[:,1]
```

### Evaluate the AdaBoost classifier


```python
# Evaluate test-set roc_auc_score
ada_roc_auc = roc_auc_score(y_test, y_pred_proba)

# Print roc_auc_score
print('ROC AUC score: {:.2f}'.format(ada_roc_auc))
```

    ROC AUC score: 0.65

