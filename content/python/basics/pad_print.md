---
title: "Print string at a fixed width"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
a_string = "abc"
fixed_string = "{0:>5}".format(a_string)
print(f'|{fixed_string}|')
```

    |  abc|

