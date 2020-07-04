---
title: "Read and write a file"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Read a file


```python
# Open "alice.txt" and assign the file to "file"
with open('alice.txt') as file:
  text = file.read()

print(text)
```

    this is alice.txt counting how many CATS i have. yes i said cAts . Not just one cat , but many catS !



```python

```
