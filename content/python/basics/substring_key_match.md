---
title: "Substring key match in a dictionary"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Using `items()` + list comprehension


```python
test_dict = {'All' : 1, 'have' : 2, 'good' : 3, 'food' : 4} 
search_key = 'ood'
res = [val for key, val in test_dict.items() if search_key in key] 
res
```




    [3, 4]


