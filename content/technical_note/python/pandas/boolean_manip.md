---
title: "Boolean operators with Pandas"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---


### Generate some data


```python
import pandas as pd

# Build cars DataFrame
names = ['United States', 'Australia', 'Japan', 'India', 'Russia', 'Morocco', 'Egypt']
dr =  [True, False, False, False, True, True, True]
cpc = [809, 731, 588, 18, 200, 70, 45]
row_labels = ['US', 'AUS', 'JPN', 'IN', 'RU', 'MOR', 'EG']
cars_dict = {'country':names, 'drives_right':dr, 'cars_per_cap':cpc }
cars = pd.DataFrame(cars_dict)
cars.index = row_labels
print(cars)
```

               country  drives_right  cars_per_cap
    US   United States          True           809
    AUS      Australia         False           731
    JPN          Japan         False           588
    IN           India         False            18
    RU          Russia          True           200
    MOR        Morocco          True            70
    EG           Egypt          True            45



```python
cars[cars['drives_right']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>drives_right</th>
      <th>cars_per_cap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>US</th>
      <td>United States</td>
      <td>True</td>
      <td>809</td>
    </tr>
    <tr>
      <th>RU</th>
      <td>Russia</td>
      <td>True</td>
      <td>200</td>
    </tr>
    <tr>
      <th>MOR</th>
      <td>Morocco</td>
      <td>True</td>
      <td>70</td>
    </tr>
    <tr>
      <th>EG</th>
      <td>Egypt</td>
      <td>True</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python
import numpy as np
cpc = cars['cars_per_cap']
between = np.logical_and(cpc>100,cpc<500)
medium = cars[between]
print(medium)
```

       country  drives_right  cars_per_cap
    RU  Russia          True           200



```python

```
