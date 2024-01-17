---
title: "Convolutions from scratch"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Discrete convolution in 1D

$y = x * w  \to y[i] = \sum\limits_{k=-\infty}^{+\infty} x[i-k] w[k]$

In practice, we cannot sum through $-\infty \to +\infty$. Instead, we pad with a finite number of zeros, called *zero-padding*. For an input **x** and filter **w** with *n* and *m* elements respectively, where $ m \leq n $. The padded vector $x^p$ has size $n + 2p$. To compute the convolution:

$y = x * w  \to y[i] = \sum\limits_{k=0}^{k=m-1} x^p[i+m-k] w[k]$

Note that **x** and **w** are indexed in different directions. To simplify the computation, flip one of the vectors and perform a dot product.


#### Size of convolution output


$o = \lfloor \frac{n + 2p - m}{s} \rfloor + 1$  


where $\lfloor . \rfloor$ is the floor operation.



```python
import numpy as np

def conv1d(x, w, p=0, s=1):
    w_rot = np.array(w[::-1])
    x_padded = np.array(x)
    if p > 0:
        zero_pad = np.zeros(shape=p)
        x_padded = np.concatenate(
            [zero_pad, x_padded, zero_pad])
    res = []
    for i in range(0, int((len(x_padded) - len(w_rot)) / s) + 1, s):
        res.append(np.sum(
            x_padded[i:i+w_rot.shape[0]] * w_rot))
        # Same as dot product:
        #res.append(np.dot(
        #    x_padded[i:i+w_rot.shape[0]],w_rot))
    return np.array(res)


## Testing:
x = [1, 3, 2, 4, 5, 6, 1, 3]
w = [1, 0, 3, 1, 2]

print('Conv1d Implementation:',
      conv1d(x, w, p=2, s=1))

print('Numpy Results:',
      np.convolve(x, w, mode='same')) 
```

    Conv1d Implementation: [ 5. 14. 16. 26. 24. 34. 19. 22.]
    Numpy Results: [ 5 14 16 26 24 34 19 22]


### Discrete convolution in 2D

$Y = X * W  \to Y[i,j] = \sum\limits_{k_1=-\infty}^{+\infty}  \sum\limits_{k_2=-\infty}^{+\infty} X[i-k_1,j-k_2]  W[k_1, k_2]$


```python
np.zeros((2,3))
```




    array([[0., 0., 0.],
           [0., 0., 0.]])




```python
def conv2d(X, W, p=(1,1), s=(1,1)):

    # Rotate rows and columns of the kernel matrix
    W_rot = np.array(W)[::-1,::-1]
    # convert to numpy array
    X_input = np.array(X)
    # Pad with zeros the n + 2p
    X_pad = np.zeros( (2*p[0] + X_input.shape[0], 2*p[1] + X_input.shape[1]))
    # Replace the core of the padded zero matrix with the actual values
    X_pad[p[0]:p[0]+X_input.shape[0], p[1]:p[1]+X_input.shape[1]] = X_input
    
    # Build the output matrix after convolutions
    res = []
    for k1 in range(0, int((X_pad.shape[0]-W_rot.shape[0])/s[0]) + 1, s[0] ):
        res.append([])
        for k2 in range(0, int((X_pad.shape[1]-W_rot.shape[1])/s[1]) + 1, s[1] ):
            res[-1].append(
                np.sum(X_pad[k1:k1+W_rot.shape[0],k2:k2+W_rot.shape[1]] *  W_rot)
            )
            
    return np.array(res)
            
```


```python

## Testing:
X = [[1, 3, 2, 4], [5, 6, 1, 3], [1, 2, 0, 2], [3, 4, 3, 2]]
W = [[1, 0, 3], [1, 2, 1], [0, 1, 1]]
p=(1,1)
s=(1,1)
print(f'Expected Dimensions: ({int((len(X) + 2*p[0] - len(W))/s[0]) + 1},{int((len(X[0]) + 2*p[1] - len(W[0]))/s[1]) + 1})')

print('Conv2d Implementation:\n',
    conv2d(X, W, p, s))

import scipy.signal
print('SciPy Results:\n',
    scipy.signal.convolve2d(X, W, mode='same'))
```

    Expected Dimensions: (4,4)
    Conv2d Implementation:
     [[11. 25. 32. 13.]
     [19. 25. 24. 13.]
     [13. 28. 25. 17.]
     [11. 17. 14.  9.]]
    SciPy Results:
     [[11 25 32 13]
     [19 25 24 13]
     [13 28 25 17]
     [11 17 14  9]]

