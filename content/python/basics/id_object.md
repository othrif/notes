---
title: "id() of an object"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Everything in python is an object. `id(object)` function returns the identity of the object. This is an integer that is unique for the given object and remains constant during its lifetime.


```python
print('id of 5 =',id(5))

a = 5
print('id of a =',id(a))

b = a
print('id of b =',id(b))

c = 5.0
print('id of c =',id(c))
```

    id of 5 = 4483840576
    id of a = 4483840576
    id of b = 4483840576
    id of c = 4518905328

