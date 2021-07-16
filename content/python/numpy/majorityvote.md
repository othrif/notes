---
title: "Majority vote: argmax, bincount, average"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Weighted majority vote


```python
import numpy as np

np.argmax(np.bincount([0, 0, 1], weights=[0.2, 0.2, 0.6]))
```




    1



### Weighted majority vote based on class probabilities

Assuming a binary classifier $i \in \{0,1\}$ and an ensemble of three classifiers $C_j \left(j \in \{1,2,3\} \right)$


```python
prob_output = np.array([[0.9, 0.1],
               [0.8, 0.2],
               [0.4, 0.6]])

# p(i_0|x) = 0.2x0.9 + 0.2x0.8 + 0.6x0.4 = 0.58
p = np.average(prob_output, 
               axis=0, 
               weights=[0.2, 0.2, 0.6])
p
```




    array([0.58, 0.42])




```python
np.argmax(p)
```




    0




```python

```
