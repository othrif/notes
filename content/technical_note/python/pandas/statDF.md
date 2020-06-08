---
title: "DataFrames statistics"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Most common summary statistics: 
- `.mean()`
- `.std()`
- `.var()`
- `.median()`
- `.mode()`
- `.min()`
- `.max()`
- `.sum()`
- `.quantile()`

### Generate some data


```python
import pandas as pd
import numpy as np
from pandas import Timestamp

mycols = ['store', 'type', 'department', 'date', 'weekly_sales', 'is_holiday']
content = np.array([[1, 'A', 1, Timestamp('2010-02-05 00:00:00'), 24924.5, False],[1, 'A', 1, Timestamp('2010-03-05 00:00:00'), 21827.9, False],[1, 'A', 1, Timestamp('2010-04-02 00:00:00'), 57258.43, False],[1, 'A', 1, Timestamp('2010-05-07 00:00:00'), 17413.94, False],[1, 'A', 1, Timestamp('2010-06-04 00:00:00'), 17558.09, False],[1, 'A', 1, Timestamp('2010-07-02 00:00:00'), 16333.14, False],[1, 'A', 1, Timestamp('2010-08-06 00:00:00'), 17508.41, False],[1, 'A', 1, Timestamp('2010-09-03 00:00:00'), 16241.78, False],[1, 'A', 1, Timestamp('2010-10-01 00:00:00'), 20094.19, False],[1, 'A', 1, Timestamp('2010-11-05 00:00:00'), 34238.88, False],[1, 'A', 1, Timestamp('2010-12-03 00:00:00'), 22517.56, False],[1, 'A', 1, Timestamp('2011-01-07 00:00:00'), 15984.24, False],[1, 'A', 2, Timestamp('2010-02-05 00:00:00'), 50605.27, False],[1, 'A', 2, Timestamp('2010-03-05 00:00:00'), 48397.98, False],[1, 'A', 2, Timestamp('2010-04-02 00:00:00'), 47450.5, False],[1, 'A', 2, Timestamp('2010-05-07 00:00:00'), 47903.01, False],[1, 'A', 2, Timestamp('2010-06-04 00:00:00'), 48754.47, False],[1, 'A', 2, Timestamp('2010-07-02 00:00:00'), 47077.72, False],[1, 'A', 2, Timestamp('2010-08-06 00:00:00'), 50031.73, False],[1, 'A', 2, Timestamp('2010-09-03 00:00:00'), 49015.05, False],[1, 'A', 2, Timestamp('2010-10-01 00:00:00'), 45829.02, False],[1, 'A', 2, Timestamp('2010-11-05 00:00:00'), 46381.43, False],[1, 'A', 2, Timestamp('2010-12-03 00:00:00'), 44405.02, False],[1, 'A', 2, Timestamp('2011-01-07 00:00:00'), 43202.29, False],[1, 'A', 3, Timestamp('2010-02-05 00:00:00'), 13740.12, False],[1, 'A', 3, Timestamp('2010-03-05 00:00:00'), 12275.58, False],[1, 'A', 3, Timestamp('2010-04-02 00:00:00'), 11157.08, False],[1, 'A', 3, Timestamp('2010-05-07 00:00:00'), 9372.8, False],[1, 'A', 3, Timestamp('2010-06-04 00:00:00'), 8001.41, False],[1, 'A', 3, Timestamp('2010-07-02 00:00:00'), 7857.88, False],[1, 'A', 3, Timestamp('2010-08-06 00:00:00'), 26719.02, False],[1, 'A', 3, Timestamp('2010-09-03 00:00:00'), 19081.8, False],[1, 'A', 3, Timestamp('2010-10-01 00:00:00'), 9775.17, False],[1, 'A', 3, Timestamp('2010-11-05 00:00:00'), 9825.22, False],[1, 'A', 3, Timestamp('2010-12-03 00:00:00'), 10856.85, False],[1, 'A', 3, Timestamp('2011-01-07 00:00:00'), 15808.15, False],[1, 'A', 4, Timestamp('2010-02-05 00:00:00'), 39954.04, False],[1, 'A', 4, Timestamp('2010-03-05 00:00:00'), 38086.19, False],[1, 'A', 4, Timestamp('2010-04-02 00:00:00'), 37809.49, False],[1, 'A', 4, Timestamp('2010-05-07 00:00:00'), 37168.34, False],[1, 'A', 4, Timestamp('2010-06-04 00:00:00'), 40548.19, False],[1, 'A', 4, Timestamp('2010-07-02 00:00:00'), 39773.71, False],[1, 'A', 4, Timestamp('2010-08-06 00:00:00'), 40973.88, False],[1, 'A', 4, Timestamp('2010-09-03 00:00:00'), 38321.88, False],[1, 'A', 4, Timestamp('2010-10-01 00:00:00'), 34912.45, False],[1, 'A', 4, Timestamp('2010-11-05 00:00:00'), 37980.55, False],[1, 'A', 4, Timestamp('2010-12-03 00:00:00'), 37110.55, False],[1, 'A', 4, Timestamp('2011-01-07 00:00:00'), 37947.8, False],[1, 'A', 5, Timestamp('2010-02-05 00:00:00'), 32229.38, False],[1, 'A', 5, Timestamp('2010-03-05 00:00:00'), 23082.14, False],[1, 'A', 5, Timestamp('2010-04-02 00:00:00'), 29967.92, False],[1, 'A', 5, Timestamp('2010-05-07 00:00:00'), 19260.44, False],[1, 'A', 5, Timestamp('2010-06-04 00:00:00'), 22932.26, False],[1, 'A', 5, Timestamp('2010-07-02 00:00:00'), 18887.71, False],[1, 'A', 5, Timestamp('2010-08-06 00:00:00'), 16926.17, False],[1, 'A', 5, Timestamp('2010-09-03 00:00:00'), 15390.52, False],[1, 'A', 5, Timestamp('2010-10-01 00:00:00'), 23381.38, False],[1, 'A', 5, Timestamp('2010-11-05 00:00:00'), 23903.81, False],[1, 'A', 5, Timestamp('2010-12-03 00:00:00'), 36472.02, False],[1, 'A', 5, Timestamp('2011-01-07 00:00:00'), 22699.69, False],[1, 'A', 6, Timestamp('2010-02-05 00:00:00'), 5749.03, False],[1, 'A', 6, Timestamp('2010-03-05 00:00:00'), 4221.25, False],[1, 'A', 6, Timestamp('2010-04-02 00:00:00'), 4132.61, False],[1, 'A', 6, Timestamp('2010-05-07 00:00:00'), 7477.7, False],[1, 'A', 6, Timestamp('2010-06-04 00:00:00'), 5484.9, False],[1, 'A', 6, Timestamp('2010-07-02 00:00:00'), 4541.91, False],[1, 'A', 6, Timestamp('2010-08-06 00:00:00'), 4700.38, False],[1, 'A', 6, Timestamp('2010-09-03 00:00:00'), 3553.75, False],[1, 'A', 6, Timestamp('2010-10-01 00:00:00'), 2876.19, False],[1, 'A', 6, Timestamp('2010-11-05 00:00:00'), 5036.99, False],[1, 'A', 6, Timestamp('2010-12-03 00:00:00'), 6356.96, False],[1, 'A', 6, Timestamp('2011-01-07 00:00:00'), 1376.15, False],[1, 'A', 7, Timestamp('2010-02-05 00:00:00'), 21084.08, False],[1, 'A', 7, Timestamp('2010-03-05 00:00:00'), 19659.7, False],[1, 'A', 7, Timestamp('2010-04-02 00:00:00'), 22427.62, False],[1, 'A', 7, Timestamp('2010-05-07 00:00:00'), 20457.62, False],[1, 'A', 7, Timestamp('2010-06-04 00:00:00'), 44563.68, False],[1, 'A', 7, Timestamp('2010-07-02 00:00:00'), 22589.0, False],[1, 'A', 7, Timestamp('2010-08-06 00:00:00'), 21842.57, False],[1, 'A', 7, Timestamp('2010-09-03 00:00:00'), 18005.65, False],[1, 'A', 7, Timestamp('2010-10-01 00:00:00'), 16481.79, False],[1, 'A', 7, Timestamp('2010-11-05 00:00:00'), 19136.58, False],[1, 'A', 7, Timestamp('2010-12-03 00:00:00'), 47406.83, False],[1, 'A', 7, Timestamp('2011-01-07 00:00:00'), 17516.16, False],[1, 'A', 8, Timestamp('2010-02-05 00:00:00'), 40129.01, False],[1, 'A', 8, Timestamp('2010-03-05 00:00:00'), 38776.09, False],[1, 'A', 8, Timestamp('2010-04-02 00:00:00'), 38151.58, False],[1, 'A', 8, Timestamp('2010-05-07 00:00:00'), 35393.78, False],[1, 'A', 8, Timestamp('2010-06-04 00:00:00'), 35181.47, False],[1, 'A', 8, Timestamp('2010-07-02 00:00:00'), 35580.01, False],[1, 'A', 8, Timestamp('2010-08-06 00:00:00'), 34833.35, False],[1, 'A', 8, Timestamp('2010-09-03 00:00:00'), 35562.68, False],[1, 'A', 8, Timestamp('2010-10-01 00:00:00'), 34658.25, False],[1, 'A', 8, Timestamp('2010-11-05 00:00:00'), 36182.58, False],[1, 'A', 8, Timestamp('2010-12-03 00:00:00'), 36222.74, False],[1, 'A', 8, Timestamp('2011-01-07 00:00:00'), 36599.46, False],[1, 'A', 9, Timestamp('2010-02-05 00:00:00'), 16930.99, False],[1, 'A', 9, Timestamp('2010-03-05 00:00:00'), 24064.7, False],[1, 'A', 9, Timestamp('2010-04-02 00:00:00'), 25435.02, False],[1, 'A', 9, Timestamp('2010-05-07 00:00:00'), 27588.34, False]])
df = pd.DataFrame(content, columns=mycols)
df['frac_sales'] = df['weekly_sales']*np.random.rand()
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
      <th>frac_sales</th>
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
      <td>10462.7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>2010-03-05</td>
      <td>21827.9</td>
      <td>False</td>
      <td>9162.84</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>2010-04-02</td>
      <td>57258.4</td>
      <td>False</td>
      <td>24035.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>2010-05-07</td>
      <td>17413.9</td>
      <td>False</td>
      <td>7309.96</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>2010-06-04</td>
      <td>17558.1</td>
      <td>False</td>
      <td>7370.47</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['weekly_sales'].mean()
```




    26291.1529




```python
df['weekly_sales'].sum()*1e-6 # in millions
```




    2.62911529




```python
df.sort_values('weekly_sales',ascending=False).head()
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
      <th>2</th>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>2010-04-02</td>
      <td>57258.4</td>
      <td>False</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>2010-02-05</td>
      <td>50605.3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>2010-08-06</td>
      <td>50031.7</td>
      <td>False</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>2010-09-03</td>
      <td>49015.1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>2010-06-04</td>
      <td>48754.5</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



### Efficient summaries with `.agg()`
`.agg()` method allows you to apply your own custom functions to a DataFrame, as well as apply functions to more than one column of a DataFrame at once, making your aggregations super efficient.


```python
# A custom inter-quartile range function. Alternative to standard deviation that is helpful if your data contains outliers
def iqr(column):
    return column.quantile(0.75) - column.quantile(0.25)

print(iqr(df['weekly_sales']))
print(df['weekly_sales'].agg(iqr))
```

    21645.687500000004
    21645.687500000004



```python
print(df[['weekly_sales','frac_sales']].agg(iqr))
```

    weekly_sales    21645.687500
    frac_sales       9086.348194
    dtype: float64



```python
print(df[['weekly_sales','frac_sales']].agg([iqr,np.median]))
```

            weekly_sales   frac_sales
    iqr       21645.6875  9086.348194
    median    23231.7600  9752.143956


### Cumulative statistics
- `.cumsum()`
- `.cummax()`


```python
df['cum_weekly_sales'] = df['weekly_sales'].cumsum()
```


```python
df['cum_max_sales'] = df['weekly_sales'].cummax()
```


```python
print(df[['date','weekly_sales','cum_weekly_sales','cum_max_sales']])
```

             date weekly_sales cum_weekly_sales cum_max_sales
    0  2010-02-05      24924.5          24924.5       24924.5
    1  2010-03-05      21827.9          46752.4       24924.5
    2  2010-04-02      57258.4           104011       57258.4
    3  2010-05-07      17413.9           121425       57258.4
    4  2010-06-04      17558.1           138983       57258.4
    ..        ...          ...              ...           ...
    95 2011-01-07      36599.5       2.5351e+06       57258.4
    96 2010-02-05        16931      2.55203e+06       57258.4
    97 2010-03-05      24064.7      2.57609e+06       57258.4
    98 2010-04-02        25435      2.60153e+06       57258.4
    99 2010-05-07      27588.3      2.62912e+06       57258.4
    
    [100 rows x 4 columns]

