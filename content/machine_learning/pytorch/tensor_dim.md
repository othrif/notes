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


