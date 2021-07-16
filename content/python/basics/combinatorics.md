---
title: "Combinatorics"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Combinations with itertools


```python
from itertools import combinations
for _ in combinations('ABCD', 2):
    print(_)
```

    ('A', 'B')
    ('A', 'C')
    ('A', 'D')
    ('B', 'C')
    ('B', 'D')
    ('C', 'D')



```python
for _ in combinations(range(4), 3):
    print(_)
```

    (0, 1, 2)
    (0, 1, 3)
    (0, 2, 3)
    (1, 2, 3)

