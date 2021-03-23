---
title: "Increase display size"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### For columns and rows


```python
import pandas as pd
pd.set_option('display.max_colwidth', 9999)
pd.set_option('display.max_rows', 9999)
```
