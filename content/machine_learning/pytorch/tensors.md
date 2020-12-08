---
title: "Handling tensors"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import torch
```

# Tensor properties

### Create tensor from a list or an array


```python
example_tensor = torch.Tensor(
    [
     [[1, 2], [3, 4]], 
     [[5, 6], [7, 8]], 
     [[9, 0], [1, 2]]
    ]
)
```

### Initialize tensors


```python
# with ones with same shape as example tensor
torch.ones_like(example_tensor)
```




    tensor([[[1., 1.],
             [1., 1.]],
    
            [[1., 1.],
             [1., 1.]],
    
            [[1., 1.],
             [1., 1.]]])




```python
# with zeros with same shape as example tensor
torch.zeros_like(example_tensor)
```




    tensor([[[0., 0.],
             [0., 0.]],
    
            [[0., 0.],
             [0., 0.]],
    
            [[0., 0.],
             [0., 0.]]])




```python
# with random with same shape as example tensor
torch.randn_like(example_tensor)
```




    tensor([[[ 0.4581, -0.6200],
             [ 0.3037, -0.0642]],
    
            [[-1.1073, -0.1540],
             [-0.0790,  1.2929]],
    
            [[-1.9917,  1.1720],
             [-0.5316, -0.4773]]])




```python
# generate tensor with shape and device
torch.randn(2, 2, device='cpu') # Alternatively, for a GPU tensor, you'd use device='cuda'
```




    tensor([[ 0.3427, -1.3345],
            [-0.1407,  0.1086]])



### Shape of tensor


```python
example_tensor.shape
```




    torch.Size([3, 2, 2])




```python
print("shape[0] =", example_tensor.shape[0])
print("Rank =", len(example_tensor.shape))
print("Number of elements =", example_tensor.numel())
```

    shape[0] = 3
    Rank = 3
    Number of elements = 12


### Indexing tensors


```python
example_tensor[1]
```




    tensor([[5., 6.],
            [7., 8.]])



### Get scalar value of a tensor


```python
example_scalar = example_tensor[1, 1, 0]
example_scalar.item()
```




    7.0



### Device of the tensor
device is either `cuda` or `cpu`


```python
example_tensor.device
```




    device(type='cpu')




```python
# Move tensor to a new device
#new_tensor = example_tensor.to('cuda')
```

### Basic functions


```python
print("Mean:", example_tensor.mean())
print("Stdev:", example_tensor.std())
```

    Mean: tensor(4.)
    Stdev: tensor(2.9848)



```python
# average  2×2  matrix of the  3×2×2  example_tensor
example_tensor.mean(0)
# torch.mean(example_tensor, 0)
```




    tensor([[5.0000, 2.6667],
            [3.6667, 4.6667]])


