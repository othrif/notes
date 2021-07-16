---
title: "Most frequent element in a list"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
test = [6, 2, 2, 3, 4, 2, 2, 90, 2, 41]
most_frequent = max(set(test), key = test.count)
print(most_frequent)
```

    2

