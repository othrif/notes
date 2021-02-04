---
title: "Get string out of a tensor string"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### How to pass arguments to a map function


```python
import tensorflow as tf
```


```python
tf.constant('hello')
```




    <tf.Tensor: shape=(), dtype=string, numpy=b'hello'>




```python
tf.constant('hello').numpy()
```




    b'hello'




```python
tf.constant('hello').numpy().decode('utf-8')
```




    'hello'


