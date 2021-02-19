---
title: "Remove everything after a character in a string"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Using `str.split(sep, maxsplit)`


```python
# maxsplit=1 to split at first occurence
a_string = "ab-cd"
split_string = a_string.split("-", 1)


substring = split_string[0]
print(substring)
```

    ab

