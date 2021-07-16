---
title: "Handling exception: ignore"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Ignore exception


```python
try:
    print(invalid-variable)
except Exception:
    pass

print("Exception ignored")
```

    Exception ignored

