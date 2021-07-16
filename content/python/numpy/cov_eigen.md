---
title: "Covariance, Correlation, and eigenvalues"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Covariance

$\sigma_{ij} = \frac{1}{N} \sum_{k=1}^{N} \left(x_i^{(k)} - \mu_i\right)\left(x_j^{(k)} - \mu_j\right)$


```python
import numpy as np
x = np.array([[1, 2], [1, 1], [2, 0]])
cov_mat = np.cov(x.T)
cov_mat
```




    array([[ 0.33333333, -0.5       ],
           [-0.5       ,  1.        ]])



### Correlation
Pearson product-moment correlation coefficients.

$\rho_{ij} = \frac{\sigma_{ij}}{\sigma_{ii}\sigma_{jj}}$


```python
np.corrcoef(x.T)
```




    array([[ 1.       , -0.8660254],
           [-0.8660254,  1.       ]])



### Eigenvalues and eigenvectors
Two methods available `np.linalg.eigh` and `np.linalg.eig`, use `eigh` which is designed for Hermitian matrices which always returns real eigenvalues. Not guaranteed with the former.

Hermitian matrix is equal to its own conjugate transpose.


```python
eigen_vals, eigen_vecs = np.linalg.eigh(cov_mat)

print('\nEigenvalues \n%s' % eigen_vals)
print('\nEigenvectors \n%s' % eigen_vecs)
```

    
    Eigenvalues 
    [0. 2.]
    
    Eigenvectors 
    [[-0.70710678 -0.70710678]
     [-0.70710678  0.70710678]]

