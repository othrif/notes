---
title: "Class NN"
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
class ExampleModule(nn.Module):
    def __init__(self, input_dims, output_dims):
        super(ExampleModule, self).__init__()
        self.linear = nn.Linear(input_dims, output_dims)
        self.exponent = nn.Parameter(torch.tensor(1.))

    def forward(self, x):
        x = self.linear(x)

        # This is the notation for element-wise exponentiation, 
        # which matches python in general
        x = x ** self.exponent 
        
        return x
```


```python
example_model = ExampleModule(10, 2) 
list(example_model.parameters())
```




    [Parameter containing:
     tensor(1., requires_grad=True),
     Parameter containing:
     tensor([[-0.3077,  0.0289,  0.1660, -0.2750, -0.2928, -0.1247,  0.1898,  0.1587,
              -0.1698, -0.0203],
             [ 0.3117, -0.1055,  0.0094, -0.0133, -0.0934,  0.0832,  0.1384,  0.1527,
               0.1605,  0.0006]], requires_grad=True),
     Parameter containing:
     tensor([-0.0879,  0.1471], requires_grad=True)]




```python
input = torch.randn(3, 10) # n x input dims
example_model(input)
```




    tensor([[-4.3126e-01,  1.1191e-03],
            [ 1.8901e-01, -3.0941e-01],
            [ 1.6205e+00, -3.4563e-01]], grad_fn=<PowBackward1>)


