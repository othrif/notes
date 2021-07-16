---
title: "Linear scikit-learn classifiers"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Basic linear supervised learning algorithms

* Perceptron
* Linear regression
* Support vector Machine


```python
from sklearn.linear_model import SGDClassifier

ppn = SGDClassifier(loss='perceptron')
lr = SGDClassifier(loss='log')
svm = SGDClassifier(loss='hinge')
```

### Basic pipeline

#### Collect data


```python
from sklearn import datasets
import numpy as np

iris = datasets.load_iris()
X = iris.data[:, [2, 3]]
y = iris.target

print('Class labels:', np.unique(y))
```

    Class labels: [0 1 2]


#### Split data


```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=1, stratify=y)

print('Labels count in y:', np.bincount(y))
print('Labels count in y_train:', np.bincount(y_train))
print('Labels count in y_test:', np.bincount(y_test))
```

    Labels count in y: [50 50 50]
    Labels count in y_train: [35 35 35]
    Labels count in y_test: [15 15 15]


#### Standardize the features


```python
from sklearn.preprocessing import StandardScaler

sc = StandardScaler()
sc.fit(X_train)
X_train_std = sc.transform(X_train)
X_test_std = sc.transform(X_test)
```

#### Train and test an algorithm


```python
svm.fit(X_train_std, y_train)
y_pred = svm.predict(X_test_std)
```


```python
from sklearn.metrics import accuracy_score
print(f'Accuracy: {accuracy_score(y_test, y_pred):.2%}')
```

    Accuracy: 93.33%


#### Visualize decision boundaries


```python
import matplotlib.pyplot as plt
from helper.plotter import plot_decision_regions

X_combined_std = np.vstack((X_train_std, X_test_std))
y_combined = np.hstack((y_train, y_test))

plot_decision_regions(X_combined_std, 
                      y_combined,
                      classifier=svm, 
                      test_idx=range(105, 150))
plt.xlabel('petal length [standardized]')
plt.ylabel('petal width [standardized]')
plt.legend(loc='upper left')
plt.tight_layout()

plt.show()
```

    /Users/othrif/github/notes/content/machine_learning/scikitlearn/helper/plotter.py:37: MatplotlibDeprecationWarning: Using a string of single character colors as a color sequence is deprecated since 3.2 and will be removed two minor releases later. Use an explicit list instead.
      plt.scatter(X_test[:, 0],



    
![png](linear_classifiers_14_1.png)
    

