---
title: "Torch tensor dimensionality"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import torch
```


```python
x = torch.randn(10,1000)
x.shape
```




    torch.Size([10, 1000])



### Mean of each row at the time in tensor form


```python
y = x.mean(1)[:, None]
y.shape
```




    torch.Size([10, 1])



### Mean each row at the time in vector form


```python
z = x.mean(1)
z.shape
```




    torch.Size([10])



### Re-arange matrix dimensions


```python
torch.arange(0,6).view(2,3)
```




    tensor([[0, 1, 2],
            [3, 4, 5]])


