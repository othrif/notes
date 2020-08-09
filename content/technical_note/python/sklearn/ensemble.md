---
title: "Ensemble learning with Voting Classifier"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
- Train different models on the same dataset  
- Let each model make its predictions
- Meta-model: aggregates predictions of individual models
- Final prediction: more robust and less prone to errors
- Best results: models are skillful in different ways.

### Import modules


```python
# Manipulation
import numpy as np
import pandas as pd
# Manipulation
import seaborn as sns
import matplotlib.pyplot as plt
# Selection
from sklearn.model_selection import train_test_split
from sklearn.model_selection import cross_val_score
# Metrics
from sklearn.metrics import accuracy_score
from sklearn.metrics import mean_squared_error as MSE
# Models
from sklearn.tree import DecisionTreeClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.neighbors import KNeighborsClassifier as KNN
# Ensemble
from sklearn.ensemble import VotingClassifier
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

### Define the ensemble


```python
# Set seed for reproducibility
SEED=1

# Instantiate lr
lr = LogisticRegression(random_state=SEED)

# Instantiate knn
knn = KNN(n_neighbors=27)

# Instantiate dt
dt = DecisionTreeClassifier(min_samples_leaf=0.13, random_state=SEED)

# Define the list classifiers
classifiers = [('Logistic Regression', lr), ('K Nearest Neighbours', knn), ('Classification Tree', dt)]
```

### Evaluate individual classifiers


```python
# Iterate over the pre-defined list of classifiers
for clf_name, clf in classifiers:    
 
    # Fit clf to the training set
    clf.fit(X_train, y_train)    
   
    # Predict y_pred
    y_pred = clf.predict(X_test)
    
    # Calculate accuracy
    accuracy = accuracy_score(y_test, y_pred) 
   
    # Evaluate clf's accuracy on the test set
    print('{:s} : {:.3f}'.format(clf_name, accuracy))
```

    Logistic Regression : 0.886
    K Nearest Neighbours : 0.912
    Classification Tree : 0.904



```python
# Instantiate a VotingClassifier vc
vc = VotingClassifier(estimators=classifiers)     

# Fit vc to the training set
vc.fit(X_train, y_train)   

# Evaluate the test set predictions
y_pred = vc.predict(X_test)

# Calculate accuracy score
accuracy = accuracy_score(y_test, y_pred)
print('Voting Classifier: {:.3f}'.format(accuracy))
```

    Voting Classifier: 0.912

