---
title: "Reading and writing CSVs"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
CSV = comma-seperated-values

#### CSV to DataFrame


```python
import pandas as pd
cars = pd.read_csv('cars.csv',index_col=0)
print(cars)
```

             country  drives_right  cars_per_cap
    0  United States          True           809
    1      Australia         False           731
    2          Japan         False           588
    3          India         False            18
    4         Russia          True           200
    5        Morocco          True            70
    6          Egypt          True            45


### Manipulate DataFrame


```python
import numpy as np
cars['cars_rand'] = cars['cars_per_cap']*np.random.randint(0,10)
print(cars)
```

             country  drives_right  cars_per_cap  cars_rand
    0  United States          True           809       3236
    1      Australia         False           731       2924
    2          Japan         False           588       2352
    3          India         False            18         72
    4         Russia          True           200        800
    5        Morocco          True            70        280
    6          Egypt          True            45        180


### DataFrame to csv


```python
cars.to_csv('cars.csv')
print(cars)
```

             country  drives_right  cars_per_cap  cars_rand
    0  United States          True           809       3236
    1      Australia         False           731       2924
    2          Japan         False           588       2352
    3          India         False            18         72
    4         Russia          True           200        800
    5        Morocco          True            70        280
    6          Egypt          True            45        180

