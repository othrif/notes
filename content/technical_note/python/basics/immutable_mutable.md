---
title: "Immutable or mutable?"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Immutable   | Mutable 
----------  |----------
 `int`      | `list`   
 `float`    | `dict`   
 `bool`     | `set`   
 `string`   | `bytearray`  
 `bytes`    | `objects`  
 `tuple`    | `functions`  
 `frozenset`| almost everything else  
 `None`     |  

First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell

### Best practice for default arguments


```python
import pandas as pd
# Use an immutable variable for the default argument 
def better_add_column(values, df=None):
  """Add a column of `values` to a DataFrame `df`."""
  # Update the function to create a default DataFrame
  if df is None:
    df = pandas.DataFrame()
  df['col_{}'.format(len(df.columns))] = values
  return df
```

We cannot define the function as: `def better_add_column(values, df=pandas.DataFrame()):` . It does not work since the code used a mutable variable as a default argument value which gives unexpected behavior


```python

```
