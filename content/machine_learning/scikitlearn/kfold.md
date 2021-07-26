---
title: "K-fold cross-validation"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Basic pipeline


```python
import pandas as pd
from sklearn.preprocessing import LabelEncoder
from sklearn.model_selection import train_test_split

df = pd.read_csv('https://archive.ics.uci.edu/ml/'
                 'machine-learning-databases'
                 '/breast-cancer-wisconsin/wdbc.data', header=None)

X = df.loc[:, 2:].values
y = df.loc[:, 1].values
le = LabelEncoder()
y = le.fit_transform(y)

X_train, X_test, y_train, y_test = \
    train_test_split(X, y, 
                     test_size=0.20,
                     stratify=y,
                     random_state=1)

```

### Combining transformers and estimators in a pipeline


```python
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
from sklearn.linear_model import LogisticRegression
from sklearn.pipeline import make_pipeline

pipe_lr = make_pipeline(StandardScaler(),
                        PCA(n_components=2),
                        LogisticRegression(random_state=1, solver='lbfgs'))

pipe_lr.fit(X_train, y_train)
y_pred = pipe_lr.predict(X_test)
print('Test Accuracy: %.3f' % pipe_lr.score(X_test, y_test))
```

    Test Accuracy: 0.956


### Scikit-learn method


```python
from sklearn.model_selection import cross_val_score

scores = cross_val_score(estimator=pipe_lr,
                         X=X_train,
                         y=y_train,
                         cv=10,
                         n_jobs=1)
print('CV accuracy scores: %s' % scores)
print('CV accuracy: %.3f +/- %.3f' % (np.mean(scores), np.std(scores)))
```

    CV accuracy scores: [0.93478261 0.93478261 0.95652174 0.95652174 0.93478261 0.95555556
     0.97777778 0.93333333 0.95555556 0.95555556]
    CV accuracy: 0.950 +/- 0.014


### k-fold Algorithm


```python
import numpy as np
from sklearn.model_selection import StratifiedKFold
    

kfold = StratifiedKFold(n_splits=10).split(X_train, y_train)

scores = []
for k, (train, test) in enumerate(kfold):
    pipe_lr.fit(X_train[train], y_train[train])
    score = pipe_lr.score(X_train[test], y_train[test])
    scores.append(score)
    print('Fold: %2d, Class dist.: %s, Acc: %.3f' % (k+1,
          np.bincount(y_train[train]), score))
    
print('\nCV accuracy: %.3f +/- %.3f' % (np.mean(scores), np.std(scores)))
```

    Fold:  1, Class dist.: [256 153], Acc: 0.935
    Fold:  2, Class dist.: [256 153], Acc: 0.935
    Fold:  3, Class dist.: [256 153], Acc: 0.957
    Fold:  4, Class dist.: [256 153], Acc: 0.957
    Fold:  5, Class dist.: [256 153], Acc: 0.935
    Fold:  6, Class dist.: [257 153], Acc: 0.956
    Fold:  7, Class dist.: [257 153], Acc: 0.978
    Fold:  8, Class dist.: [257 153], Acc: 0.933
    Fold:  9, Class dist.: [257 153], Acc: 0.956
    Fold: 10, Class dist.: [257 153], Acc: 0.956
    
    CV accuracy: 0.950 +/- 0.014

