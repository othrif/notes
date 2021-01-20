---
title: "Pass arguments to TF map using lambda"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### How to pass arguments to a map function


```python
import tensorflow as tf
def fun(x, arg):
    return x * arg

my_arg = tf.constant(2, dtype=tf.int64)
ds = tf.data.Dataset.range(5)
ds = ds.map(lambda x: fun(x, my_arg))
```
