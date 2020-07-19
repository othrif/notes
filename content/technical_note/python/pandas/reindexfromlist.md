---
title: "Reindexing DataFrame from a list"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
months = ['Apr', 'Jul', 'Jan', 'Oct']
temp = [61.956044, 68.934783, 32.133333, 43.434783]
mytemp = {'Mean TemperatureF': temp}
weather1 = pd.DataFrame(mytemp)
weather1.index=months
print(weather1)

```

         Mean TemperatureF
    Apr          61.956044
    Jul          68.934783
    Jan          32.133333
    Oct          43.434783



```python
year = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec']

```


```python
# Import pandas
import pandas as pd

# Reindex weather1 using the list year: weather2
weather2 = weather1.reindex(year)

# Print weather2
print(weather2)

# Reindex weather1 using the list year with forward-fill: weather3
weather3 = weather1.reindex(year).ffill()

# Print weather3
print(weather3)
```

         Mean TemperatureF
    Jan          32.133333
    Feb                NaN
    Mar                NaN
    Apr          61.956044
    May                NaN
    Jun                NaN
    Jul          68.934783
    Aug                NaN
    Sep                NaN
    Oct          43.434783
    Nov                NaN
    Dec                NaN
         Mean TemperatureF
    Jan          32.133333
    Feb          32.133333
    Mar          32.133333
    Apr          61.956044
    May          61.956044
    Jun          61.956044
    Jul          68.934783
    Aug          68.934783
    Sep          68.934783
    Oct          43.434783
    Nov          43.434783
    Dec          43.434783



```python

```
