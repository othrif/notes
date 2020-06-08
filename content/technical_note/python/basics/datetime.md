---
title: "Datetime"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Convert string to datetime
`datetime.strptime(date_string, format)`


```python
from datetime import datetime
date_string='03/01/2019 12:00:00 AM'
datetime.strptime(date_string, '%m/%d/%Y %I:%M:%S %p')
```




    datetime.datetime(2019, 3, 1, 0, 0)



### Find last month


```python
import datetime
today = datetime.date.today()
print(today)
first = today.replace(day=1)
print(first)
lastMonth = first - datetime.timedelta(days=1)
print(lastMonth)
```

    2020-05-17
    2020-05-01
    2020-04-30


### Count number of months


```python
def diff_month(d1, d2):
    return (d1.year - d2.year) * 12 + d1.month - d2.month
num_months = diff_month(first,lastMonth)
print(num_months)
num_months = diff_month(today,first)
print(num_months)
```

    1
    0



```python

```
