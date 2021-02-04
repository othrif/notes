---
title: "Manipulate maps"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Loop over map elements


```python
prices = {'apple': 0.40, 'orange': 0.35, 'banana': 0.25}
for k, v in prices.items():
    prices[k] = round(v * 0.9, 2)
prices
```




    {'apple': 0.36, 'orange': 0.32, 'banana': 0.23}


