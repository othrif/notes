---
title: "Ensemble learning with Bagging"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
- Bagging: Bootstrap Aggregation
    - one algorithm
    - Different subsets of the training set
- Uses a technique known as the bootstrap
- Reduces variance of individual models in the ensemble

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
from sklearn.metrics import accuracy_score
# Models
from sklearn.tree import DecisionTreeClassifier
# Ensemble
from sklearn.ensemble import BaggingClassifier
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

### Define the bagging classifier


```python
# Instantiate dt
dt = DecisionTreeClassifier(random_state=SEED)

# Instantiate bc
bc = BaggingClassifier(base_estimator=dt, n_estimators=50, random_state=SEED)
```

### Evaluate bagging performance


```python
# Fit bc to the training set
bc.fit(X_train, y_train)

# Predict test set labels
y_pred = bc.predict(X_test)

# Evaluate acc_test
acc_test = accuracy_score(y_test, y_pred)
print('Test set accuracy of bc: {:.2f}'.format(acc_test)) 
```

    Test set accuracy of bc: 0.71



```python
# Fit single tree to the training set
dt.fit(X_train, y_train)

# Predict test set labels
y_pred_singleTree = dt.predict(X_test)

# Evaluate acc_test
acc_test_singleTree = accuracy_score(y_test, y_pred)
print('Test set accuracy of single tree: {:.2f}'.format(acc_test)) 
```

    Test set accuracy of single tree: 0.63


A single tree achieved 8% lower accuracy than bagging! 

#### Evaluate Out of Box (OOB) accuracy
- On average, for each model, 63% of the training instances are sampled when bootstrapping
- The remaining 37% constitute the OOB instances.



```python
# Instantiate dt
dt = DecisionTreeClassifier(min_samples_leaf=8, random_state=1)

# Instantiate bc
bc = BaggingClassifier(base_estimator=dt, 
            n_estimators=50,
            oob_score=True,
            random_state=1)

# Fit bc to the training set 
bc.fit(X_train, y_train)

# Predict test set labels
y_pred = bc.predict(X_test)

# Evaluate test set accuracy
acc_test = accuracy_score(y_test, y_pred)

# Evaluate OOB accuracy
acc_oob = bc.oob_score_

# Print acc_test and acc_oob
print('Test set accuracy: {:.3f}, OOB accuracy: {:.3f}'.format(acc_test, acc_oob))
```

    Test set accuracy: 0.690, OOB accuracy: 0.708


The test set accuracy and the OOB accuracy of bc are both roughly equal to 70%!


```python

```
