---
title: "Rename columns"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Rename column


```python
import pandas as pd
df = pd.DataFrame({"num": [1, 2], "let": ["a", "b"]})
print(df)
```

       num let
    0    1   a
    1    2   b



```python
df.rename({"num": "number", "let": "letter"}, axis="columns", inplace=True)
print(df)
```

       number letter
    0       1      a
    1       2      b


### Apply function to all column names


```python
df = pd.DataFrame({"some place": ["hawaii", "costa rica"], "fun activity": ["surfing", "zip lining"]})
print(df)
```

       some place fun activity
    0      hawaii      surfing
    1  costa rica   zip lining



```python
df.rename(lambda x: x.replace(" ", "_"), axis="columns", inplace=True)
print(df)
```

       some_place fun_activity
    0      hawaii      surfing
    1  costa rica   zip lining

