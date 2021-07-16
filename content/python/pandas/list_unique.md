---
title: "List unique values in a pandas column"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Preliminaries


```python
# Import modules
import pandas as pd

# Set ipython's max row display
pd.set_option('display.max_row', 1000)

# Set iPython's max column width to 50
pd.set_option('display.max_columns', 50)
```

### Create an example dataframe


```python
# Create an example dataframe
data = {'name': ['Jason', 'Molly', 'Tina', 'Jake', 'Amy'], 
        'year': [2012, 2012, 2013, 2014, 2014], 
        'reports': [4, 24, 31, 2, 3]}
df = pd.DataFrame(data, index = ['Cochice', 'Pima', 'Santa Cruz', 'Maricopa', 'Yuma'])
df
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
      <th>name</th>
      <th>year</th>
      <th>reports</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Cochice</th>
      <td>Jason</td>
      <td>2012</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Pima</th>
      <td>Molly</td>
      <td>2012</td>
      <td>24</td>
    </tr>
    <tr>
      <th>Santa Cruz</th>
      <td>Tina</td>
      <td>2013</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Maricopa</th>
      <td>Jake</td>
      <td>2014</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Yuma</th>
      <td>Amy</td>
      <td>2014</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



### List unique values


```python
#List unique values in the df['name'] column
df.name.unique()
```




    array(['Jason', 'Molly', 'Tina', 'Jake', 'Amy'], dtype=object)


