---
title: "Basics of building a MLP"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import torch
import torch.nn as nn
```


```python
# Performs the operation  𝐴𝑥+𝑏 , where  𝐴  and  𝑏  are initialized randomly
linear = nn.Linear(10, 2) # nn.Linear(input dim=10, output dim=2) will take in a  𝑛×10  matrix and return an  𝑛×2  matrix 
example_input = torch.randn(3, 10)
example_output = linear(example_input)
example_output
```




    tensor([[ 0.5458,  0.1715],
            [ 0.0310, -0.2061],
            [ 1.3804, -0.1380]], grad_fn=<AddmmBackward>)




```python
# ReLU non-linearity sets all negative numbers in a tensor to zero
relu = nn.ReLU()
relu_output = relu(example_output)
relu_output
```




    tensor([[0.0000, 0.3189],
            [0.0000, 0.6577],
            [0.1315, 0.0000]], grad_fn=<ReluBackward0>)




```python
# Rescale a batch of  𝑛  inputs to have a consistent mean and standard deviation between batches
batchnorm = nn.BatchNorm1d(2)
batchnorm_output = batchnorm(relu_output)
batchnorm_output
```




    tensor([[-0.7062, -0.0247],
            [-0.7062,  1.2368],
            [ 1.4124, -1.2121]], grad_fn=<NativeBatchNormBackward>)




```python
# do it with one operation
mlp_layer = nn.Sequential(
    nn.Linear(5, 2),
    nn.ReLU(),
    nn.BatchNorm1d(2)

)

test_example = torch.randn(5,5)
print("input: ")
print(test_example)
print("output: ")
print(mlp_layer(test_example))
```

    input: 
    tensor([[ 1.4355,  0.1143,  0.0974,  0.2137,  1.9092],
            [-0.7489, -1.7915,  0.3816, -0.0109,  1.3555],
            [-1.8546, -2.9966,  0.5250, -0.4175,  1.0728],
            [ 0.5806, -0.6192, -0.0937, -1.3968,  0.8309],
            [-1.2107, -0.3949,  0.8021, -0.7953, -0.5259]])
    output: 
    tensor([[-0.8080,  1.9998],
            [-0.8080, -0.5000],
            [-0.8080, -0.5000],
            [ 0.9855, -0.5000],
            [ 1.4384, -0.5000]], grad_fn=<NativeBatchNormBackward>)



```python
# Optimizer
import torch.optim as optim
adam_opt = optim.Adam(mlp_layer.parameters(), lr=1e-1)
```


```python
train_example = torch.randn(100,5) + 1
adam_opt.zero_grad()

for i in range(10):  
    # Loss function
    cur_loss = torch.abs(1 - mlp_layer(train_example)).mean()
    cur_loss.backward()
    adam_opt.step()
    print(cur_loss)
```

    tensor(0.5653, grad_fn=<MeanBackward0>)
    tensor(0.4999, grad_fn=<MeanBackward0>)
    tensor(0.4354, grad_fn=<MeanBackward0>)
    tensor(0.3699, grad_fn=<MeanBackward0>)
    tensor(0.3009, grad_fn=<MeanBackward0>)
    tensor(0.2271, grad_fn=<MeanBackward0>)
    tensor(0.1474, grad_fn=<MeanBackward0>)
    tensor(0.0749, grad_fn=<MeanBackward0>)
    tensor(0.0687, grad_fn=<MeanBackward0>)
    tensor(0.1651, grad_fn=<MeanBackward0>)

