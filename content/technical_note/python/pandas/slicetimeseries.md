---
title: "Slicing time series"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Add the date column to the index, then use `.loc[]` to perform the subsetting. The important thing to remember is to keep your dates in ISO 8601 format, that is, `yyyy-mm-dd`.

Important: 
- When filtering with `[]` between `2010` and `2012`, the dates go from `2010-01-01` to `2012-01-01`.
- When filter with `.loc[]` is inclusive in dates, see the two cases below

#### Generate some data


```python
import pandas as pd
import numpy as np
from pandas import Timestamp

mycols = ['store', 'type', 'department', 'date', 'weekly_sales', 'is_holiday']
content = np.array([[1, 'A', 1, Timestamp('2010-02-05 00:00:00'), 24924.5, False],[1, 'B', 1, Timestamp('2010-03-05 00:00:00'), 21827.9, True],[1, 'A', 1, Timestamp('2010-04-02 00:00:00'), 57258.43, False],[1, 'C', 1, Timestamp('2010-05-07 00:00:00'), 17413.94, False],[1, 'C', 1, Timestamp('2010-06-04 00:00:00'), 17558.09, False],[1, 'C', 1, Timestamp('2010-07-02 00:00:00'), 16333.14, False],[1, 'C', 1, Timestamp('2010-08-06 00:00:00'), 17508.41, False],[1, 'B', 1, Timestamp('2010-09-03 00:00:00'), 16241.78, False],[1, 'A', 1, Timestamp('2010-10-01 00:00:00'), 20094.19, True],[1, 'B', 1, Timestamp('2010-11-05 00:00:00'), 34238.88, False],[1, 'C', 1, Timestamp('2010-12-03 00:00:00'), 22517.56, False],[1, 'A', 1, Timestamp('2011-01-07 00:00:00'), 15984.24, False],[1, 'C', 2, Timestamp('2010-02-05 00:00:00'), 50605.27, True],[1, 'A', 2, Timestamp('2010-03-05 00:00:00'), 48397.98, False],[1, 'A', 2, Timestamp('2010-04-02 00:00:00'), 47450.5, False],[1, 'A', 2, Timestamp('2010-05-07 00:00:00'), 47903.01, False],[1, 'A', 2, Timestamp('2010-06-04 00:00:00'), 48754.47, False],[1, 'A', 2, Timestamp('2010-07-02 00:00:00'), 47077.72, False],[1, 'A', 2, Timestamp('2010-08-06 00:00:00'), 50031.73, False],[1, 'A', 2, Timestamp('2010-09-03 00:00:00'), 49015.05, False],[1, 'A', 2, Timestamp('2010-10-01 00:00:00'), 45829.02, False],[1, 'A', 2, Timestamp('2010-11-05 00:00:00'), 46381.43, True],[1, 'A', 2, Timestamp('2010-12-03 00:00:00'), 44405.02, False],[1, 'A', 2, Timestamp('2011-01-07 00:00:00'), 43202.29, False],[1, 'A', 3, Timestamp('2010-02-05 00:00:00'), 13740.12, False],[1, 'A', 3, Timestamp('2010-03-05 00:00:00'), 12275.58, False],[1, 'A', 3, Timestamp('2010-04-02 00:00:00'), 11157.08, False],[1, 'A', 3, Timestamp('2010-05-07 00:00:00'), 9372.8, True],[1, 'A', 3, Timestamp('2010-06-04 00:00:00'), 8001.41, False],[1, 'C', 3, Timestamp('2010-07-02 00:00:00'), 7857.88, True],[1, 'A', 3, Timestamp('2010-08-06 00:00:00'), 26719.02, False],[1, 'A', 3, Timestamp('2010-09-03 00:00:00'), 19081.8, False],[1, 'B', 3, Timestamp('2010-10-01 00:00:00'), 9775.17, False],[1, 'A', 3, Timestamp('2010-11-05 00:00:00'), 9825.22, False],[1, 'A', 3, Timestamp('2010-12-03 00:00:00'), 10856.85, False],[1, 'A', 3, Timestamp('2011-01-07 00:00:00'), 15808.15, False],[1, 'A', 4, Timestamp('2010-02-05 00:00:00'), 39954.04, False],[1, 'A', 4, Timestamp('2010-03-05 00:00:00'), 38086.19, False],[1, 'A', 4, Timestamp('2010-04-02 00:00:00'), 37809.49, False],[1, 'A', 4, Timestamp('2010-05-07 00:00:00'), 37168.34, False],[1, 'A', 4, Timestamp('2010-06-04 00:00:00'), 40548.19, False],[1, 'B', 4, Timestamp('2010-07-02 00:00:00'), 39773.71, False],[1, 'A', 4, Timestamp('2010-08-06 00:00:00'), 40973.88, False],[1, 'A', 4, Timestamp('2010-09-03 00:00:00'), 38321.88, False],[1, 'A', 4, Timestamp('2010-10-01 00:00:00'), 34912.45, False],[1, 'A', 4, Timestamp('2010-11-05 00:00:00'), 37980.55, False],[1, 'A', 4, Timestamp('2010-12-03 00:00:00'), 37110.55, False],[1, 'A', 4, Timestamp('2011-01-07 00:00:00'), 37947.8, False],[1, 'A', 5, Timestamp('2010-02-05 00:00:00'), 32229.38, False],[1, 'A', 5, Timestamp('2010-03-05 00:00:00'), 23082.14, False],[1, 'B', 5, Timestamp('2010-04-02 00:00:00'), 29967.92, False],[1, 'A', 5, Timestamp('2010-05-07 00:00:00'), 19260.44, False],[1, 'A', 5, Timestamp('2010-06-04 00:00:00'), 22932.26, False],[1, 'A', 5, Timestamp('2010-07-02 00:00:00'), 18887.71, False],[1, 'A', 5, Timestamp('2010-08-06 00:00:00'), 16926.17, False],[1, 'A', 5, Timestamp('2010-09-03 00:00:00'), 15390.52, False],[1, 'A', 5, Timestamp('2010-10-01 00:00:00'), 23381.38, False],[1, 'A', 5, Timestamp('2010-11-05 00:00:00'), 23903.81, False],[1, 'A', 5, Timestamp('2010-12-03 00:00:00'), 36472.02, False],[1, 'A', 5, Timestamp('2011-01-07 00:00:00'), 22699.69, False],[1, 'A', 6, Timestamp('2010-02-05 00:00:00'), 5749.03, False],[1, 'A', 6, Timestamp('2010-03-05 00:00:00'), 4221.25, False],[1, 'A', 6, Timestamp('2010-04-02 00:00:00'), 4132.61, False],[1, 'A', 6, Timestamp('2010-05-07 00:00:00'), 7477.7, False],[1, 'A', 6, Timestamp('2010-06-04 00:00:00'), 5484.9, False],[1, 'A', 6, Timestamp('2010-07-02 00:00:00'), 4541.91, False],[1, 'A', 6, Timestamp('2010-08-06 00:00:00'), 4700.38, False],[1, 'A', 6, Timestamp('2010-09-03 00:00:00'), 3553.75, False],[1, 'B', 6, Timestamp('2010-10-01 00:00:00'), 2876.19, False],[1, 'A', 6, Timestamp('2010-11-05 00:00:00'), 5036.99, False],[1, 'A', 6, Timestamp('2010-12-03 00:00:00'), 6356.96, False],[1, 'A', 6, Timestamp('2011-01-07 00:00:00'), 1376.15, False],[1, 'A', 7, Timestamp('2010-02-05 00:00:00'), 21084.08, False],[1, 'A', 7, Timestamp('2010-03-05 00:00:00'), 19659.7, False],[1, 'A', 7, Timestamp('2010-04-02 00:00:00'), 22427.62, False],[1, 'A', 7, Timestamp('2010-05-07 00:00:00'), 20457.62, False],[1, 'A', 7, Timestamp('2010-06-04 00:00:00'), 44563.68, False],[1, 'A', 7, Timestamp('2010-07-02 00:00:00'), 22589.0, False],[1, 'A', 7, Timestamp('2010-08-06 00:00:00'), 21842.57, False],[1, 'A', 7, Timestamp('2010-09-03 00:00:00'), 18005.65, False],[1, 'A', 7, Timestamp('2010-10-01 00:00:00'), 16481.79, False],[1, 'A', 7, Timestamp('2010-11-05 00:00:00'), 19136.58, False],[1, 'A', 7, Timestamp('2010-12-03 00:00:00'), 47406.83, False],[1, 'A', 7, Timestamp('2011-01-07 00:00:00'), 17516.16, False],[1, 'A', 8, Timestamp('2010-02-05 00:00:00'), 40129.01, False],[1, 'A', 8, Timestamp('2010-03-05 00:00:00'), 38776.09, False],[1, 'A', 8, Timestamp('2010-04-02 00:00:00'), 38151.58, False],[1, 'A', 8, Timestamp('2010-05-07 00:00:00'), 35393.78, False],[1, 'A', 8, Timestamp('2010-06-04 00:00:00'), 35181.47, False],[1, 'A', 8, Timestamp('2010-07-02 00:00:00'), 35580.01, False],[1, 'A', 8, Timestamp('2010-08-06 00:00:00'), 34833.35, False],[1, 'A', 8, Timestamp('2010-09-03 00:00:00'), 35562.68, False],[1, 'A', 8, Timestamp('2010-10-01 00:00:00'), 34658.25, False],[1, 'A', 8, Timestamp('2010-11-05 00:00:00'), 36182.58, False],[1, 'A', 8, Timestamp('2010-12-03 00:00:00'), 36222.74, False],[1, 'A', 8, Timestamp('2011-01-07 00:00:00'), 36599.46, False],[1, 'A', 9, Timestamp('2010-02-05 00:00:00'), 16930.99, False],[1, 'A', 9, Timestamp('2010-03-05 00:00:00'), 24064.7, False],[1, 'A', 9, Timestamp('2010-04-02 00:00:00'), 25435.02, False],[1, 'A', 9, Timestamp('2010-05-07 00:00:00'), 27588.34, False]])
df = pd.DataFrame(content, columns=mycols)
```


```python
df.head()
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
      <th>store</th>
      <th>type</th>
      <th>department</th>
      <th>date</th>
      <th>weekly_sales</th>
      <th>is_holiday</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>2010-02-05</td>
      <td>24924.5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>B</td>
      <td>1</td>
      <td>2010-03-05</td>
      <td>21827.9</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>2010-04-02</td>
      <td>57258.4</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>C</td>
      <td>1</td>
      <td>2010-05-07</td>
      <td>17413.9</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>C</td>
      <td>1</td>
      <td>2010-06-04</td>
      <td>17558.1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



The time range below gives january-february, Note the real range is `2010-01-01` to `2010-03-01`


```python
df[ ('2010-01' <= df['date']) & (df['date'] < '2010-03')]
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
      <th>store</th>
      <th>type</th>
      <th>department</th>
      <th>date</th>
      <th>weekly_sales</th>
      <th>is_holiday</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>2010-02-05</td>
      <td>24924.5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1</td>
      <td>C</td>
      <td>2</td>
      <td>2010-02-05</td>
      <td>50605.3</td>
      <td>True</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1</td>
      <td>A</td>
      <td>3</td>
      <td>2010-02-05</td>
      <td>13740.1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>36</th>
      <td>1</td>
      <td>A</td>
      <td>4</td>
      <td>2010-02-05</td>
      <td>39954</td>
      <td>False</td>
    </tr>
    <tr>
      <th>48</th>
      <td>1</td>
      <td>A</td>
      <td>5</td>
      <td>2010-02-05</td>
      <td>32229.4</td>
      <td>False</td>
    </tr>
    <tr>
      <th>60</th>
      <td>1</td>
      <td>A</td>
      <td>6</td>
      <td>2010-02-05</td>
      <td>5749.03</td>
      <td>False</td>
    </tr>
    <tr>
      <th>72</th>
      <td>1</td>
      <td>A</td>
      <td>7</td>
      <td>2010-02-05</td>
      <td>21084.1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>84</th>
      <td>1</td>
      <td>A</td>
      <td>8</td>
      <td>2010-02-05</td>
      <td>40129</td>
      <td>False</td>
    </tr>
    <tr>
      <th>96</th>
      <td>1</td>
      <td>A</td>
      <td>9</td>
      <td>2010-02-05</td>
      <td>16931</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_ind = df.set_index('date').sort_index()
df_ind.loc['2010-01':'2010-03'] # loc is inclusive in dates
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
      <th>store</th>
      <th>type</th>
      <th>department</th>
      <th>weekly_sales</th>
      <th>is_holiday</th>
    </tr>
    <tr>
      <th>date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2010-02-05</th>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>24924.5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-02-05</th>
      <td>1</td>
      <td>A</td>
      <td>9</td>
      <td>16931</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-02-05</th>
      <td>1</td>
      <td>A</td>
      <td>8</td>
      <td>40129</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-02-05</th>
      <td>1</td>
      <td>A</td>
      <td>7</td>
      <td>21084.1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-02-05</th>
      <td>1</td>
      <td>A</td>
      <td>6</td>
      <td>5749.03</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-02-05</th>
      <td>1</td>
      <td>A</td>
      <td>5</td>
      <td>32229.4</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-02-05</th>
      <td>1</td>
      <td>A</td>
      <td>4</td>
      <td>39954</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-02-05</th>
      <td>1</td>
      <td>C</td>
      <td>2</td>
      <td>50605.3</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2010-02-05</th>
      <td>1</td>
      <td>A</td>
      <td>3</td>
      <td>13740.1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-03-05</th>
      <td>1</td>
      <td>A</td>
      <td>9</td>
      <td>24064.7</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-03-05</th>
      <td>1</td>
      <td>A</td>
      <td>8</td>
      <td>38776.1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-03-05</th>
      <td>1</td>
      <td>A</td>
      <td>7</td>
      <td>19659.7</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-03-05</th>
      <td>1</td>
      <td>A</td>
      <td>6</td>
      <td>4221.25</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-03-05</th>
      <td>1</td>
      <td>A</td>
      <td>4</td>
      <td>38086.2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-03-05</th>
      <td>1</td>
      <td>A</td>
      <td>3</td>
      <td>12275.6</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-03-05</th>
      <td>1</td>
      <td>A</td>
      <td>5</td>
      <td>23082.1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2010-03-05</th>
      <td>1</td>
      <td>B</td>
      <td>1</td>
      <td>21827.9</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2010-03-05</th>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>48398</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
