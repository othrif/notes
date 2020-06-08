---
title: "Enumerate a dictionary"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Enumerate through both keys and values 


```python
example_dict = {1:'a', 2:'b', 3:'c', 4:'d'}
for i, (k, v) in enumerate(example_dict.items()):
    print(i, k, v)
```

    0 1 a
    1 2 b
    2 3 c
    3 4 d

