---
title: "ROC curve for multiclass problem"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
from sklearn.metrics import roc_curve, auc
from sklearn import datasets
from sklearn.multiclass import OneVsRestClassifier
from sklearn.svm import LinearSVC
from sklearn.preprocessing import label_binarize
from sklearn.model_selection import train_test_split
import matplotlib.pyplot as plt

iris = datasets.load_iris()
X, y = iris.data, iris.target

y = label_binarize(y, classes=[0,1,2])
n_classes = 3

# shuffle and split training and test sets
X_train, X_test, y_train, y_test =\
    train_test_split(X, y, test_size=0.33, random_state=0)

# classifier
clf = OneVsRestClassifier(LinearSVC(random_state=0))
y_score = clf.fit(X_train, y_train).decision_function(X_test)

# Compute ROC curve and ROC area for each class
fpr = dict()
tpr = dict()
roc_auc = dict()
for i in range(n_classes):
    fpr[i], tpr[i], _ = roc_curve(y_test[:, i], y_score[:, i])
    roc_auc[i] = auc(fpr[i], tpr[i])

# Plot of a ROC curve for a specific class
for i in range(n_classes):
    plt.figure()
    plt.plot(fpr[i], tpr[i], label='ROC curve (area = %0.2f)' % roc_auc[i])
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('Receiver operating characteristic example')
    plt.legend(loc="lower right")
    plt.show()

```

    /Users/othrif/.pyenv/versions/3.9.6/lib/python3.9/site-packages/sklearn/svm/_base.py:985: ConvergenceWarning: Liblinear failed to converge, increase the number of iterations.
      warnings.warn("Liblinear failed to converge, increase "
    /Users/othrif/.pyenv/versions/3.9.6/lib/python3.9/site-packages/sklearn/svm/_base.py:985: ConvergenceWarning: Liblinear failed to converge, increase the number of iterations.
      warnings.warn("Liblinear failed to converge, increase "



![png](roc_multiclass_1_1.png)



![png](roc_multiclass_1_2.png)



![png](roc_multiclass_1_3.png)



```python
y_score
```




    array([[-2.76908971, -0.84815784,  1.94942999],
           [-1.46037484,  0.67190143, -1.53847278],
           [ 1.7293394 , -1.42179149, -7.80488854],
           [-3.15022547,  0.34381685,  1.3860928 ],
           [ 1.21840934, -0.70863042, -6.50287512],
           [-3.25269012, -0.93856079,  2.65442134],
           [ 1.38286123, -0.99785056, -6.77231643],
           [-1.74241753, -0.28304858, -1.14081791],
           [-1.88147293,  0.13337523, -1.00394763],
           [-1.32552243, -0.1636333 , -1.68170673],
           [-2.78001864,  0.65858721,  1.24659415],
           [-1.60130977, -0.47459117, -1.20956413],
           [-1.8666388 ,  0.27755401, -0.65657016],
           [-1.82219943, -0.08137924, -0.86631552],
           [-1.91078187, -0.02539647, -0.46074042],
           [ 1.40160781, -0.82210375, -6.83557513],
           [-1.80795065, -0.23278878, -0.5462846 ],
           [-1.8270918 ,  0.28399968, -0.33922585],
           [ 1.05679318, -0.53017297, -6.02199439],
           [ 1.58735147, -1.43388264, -7.37383558],
           [-2.47807515, -0.51562728,  1.30512716],
           [-1.85522427, -0.33302202, -0.17224099],
           [ 0.84164658, -0.52601171, -5.61729543],
           [ 0.97182837, -0.3506676 , -5.63740218],
           [-2.18011585, -0.32359442,  0.2018587 ],
           [ 1.62748382, -1.13184866, -7.02914472],
           [ 0.98236553, -1.07444568, -5.97315707],
           [-1.51380553, -0.10297547, -1.36880131],
           [-1.05521281,  0.21711517, -1.65410621],
           [ 1.05112319, -0.87857678, -6.06913555],
           [-2.6001415 , -0.24029245,  0.9209614 ],
           [-1.89878199, -0.34038418,  0.05093531],
           [ 1.30180887, -0.78677716, -6.79836039],
           [-2.20551234, -0.4507981 ,  0.33442974],
           [-2.97093797, -0.37115367,  1.83976662],
           [-1.52006516, -0.26747015, -0.6366359 ],
           [ 1.32163364, -1.03862883, -7.10795702],
           [-2.42943427,  0.11447955,  0.7260078 ],
           [-1.53998392, -0.46446443, -1.00380798],
           [-1.42855019,  0.10506205, -1.33639368],
           [-2.67884521, -0.46622158,  0.94912586],
           [ 1.23999165, -0.64364629, -6.35469441],
           [-2.36800438, -0.95547186,  0.37096406],
           [ 1.00698012, -1.18152727, -5.87330581],
           [ 1.42505021, -0.95043281, -7.16615465],
           [-1.34134077,  0.56863232, -1.10597758],
           [-2.61820446, -0.15110246,  0.88168223],
           [-2.91567091, -1.06632211,  1.71126621],
           [-2.50334964,  0.60324966,  0.78788249],
           [-3.02375958,  0.42628989,  1.51685337]])




```python
y_test
```




    array([[0, 0, 1],
           [0, 1, 0],
           [1, 0, 0],
           [0, 0, 1],
           [1, 0, 0],
           [0, 0, 1],
           [1, 0, 0],
           [0, 1, 0],
           [0, 1, 0],
           [0, 1, 0],
           [0, 0, 1],
           [0, 1, 0],
           [0, 1, 0],
           [0, 1, 0],
           [0, 1, 0],
           [1, 0, 0],
           [0, 1, 0],
           [0, 1, 0],
           [1, 0, 0],
           [1, 0, 0],
           [0, 0, 1],
           [0, 1, 0],
           [1, 0, 0],
           [1, 0, 0],
           [0, 0, 1],
           [1, 0, 0],
           [1, 0, 0],
           [0, 1, 0],
           [0, 1, 0],
           [1, 0, 0],
           [0, 0, 1],
           [0, 1, 0],
           [1, 0, 0],
           [0, 0, 1],
           [0, 0, 1],
           [0, 1, 0],
           [1, 0, 0],
           [0, 1, 0],
           [0, 1, 0],
           [0, 1, 0],
           [0, 0, 1],
           [1, 0, 0],
           [0, 0, 1],
           [1, 0, 0],
           [1, 0, 0],
           [0, 1, 0],
           [0, 0, 1],
           [0, 0, 1],
           [0, 0, 1],
           [0, 0, 1]])




```python

```
