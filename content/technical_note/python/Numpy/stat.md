---
title: "Numpy summary statistics"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import numpy as np
```

### Generate some data
Randomly sample from a nomral distribution 5000 times with give mean and standard deviation


```python
height = np.round(np.random.normal(1.75, 0.20, 5000), 2)
weight = np.round(np.random.normal(60.32, 15, 5000), 2)
np_city = np.column_stack((height, weight))
```


```python
np_city.shape
```




    (5000, 2)



###  Basics staistics


```python
np.round(np.mean(np_city[:,0]),2)
```




    1.75




```python
np.round(np.mean(np_city[:,1]),2)
```




    60.43




```python
print(np.round(np.mean(np_city,axis=0),2))
```

    [ 1.75 60.43]



```python
print(np.round(np.median(np_city,axis=0),2))
```

    [ 1.76 60.56]



```python
print(np.round(np.std(np_city,axis=0),2))
```

    [ 0.2  14.84]


### Correlation coefficient


```python
np.corrcoef(np_city[:,0], np_city[:,1])
```




    array([[1.        , 0.00446188],
           [0.00446188, 1.        ]])


