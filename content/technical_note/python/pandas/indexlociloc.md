---
title: "Slicing and subsetting with .loc and .iloc"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
#### Generate some data


```python
import pandas as pd
import numpy as np
from pandas import Timestamp

mycols = ['store', 'type', 'department', 'date', 'weekly_sales', 'is_holiday']
content = np.array([[1, 'A', 1, Timestamp('2010-02-05 00:00:00'), 24924.5, False],[1, 'B', 1, Timestamp('2010-03-05 00:00:00'), 21827.9, True],[1, 'A', 1, Timestamp('2010-04-02 00:00:00'), 57258.43, False],[1, 'C', 1, Timestamp('2010-05-07 00:00:00'), 17413.94, False],[1, 'C', 1, Timestamp('2010-06-04 00:00:00'), 17558.09, False],[1, 'C', 1, Timestamp('2010-07-02 00:00:00'), 16333.14, False],[1, 'C', 1, Timestamp('2010-08-06 00:00:00'), 17508.41, False],[1, 'B', 1, Timestamp('2010-09-03 00:00:00'), 16241.78, False],[1, 'A', 1, Timestamp('2010-10-01 00:00:00'), 20094.19, True],[1, 'B', 1, Timestamp('2010-11-05 00:00:00'), 34238.88, False],[1, 'C', 1, Timestamp('2010-12-03 00:00:00'), 22517.56, False],[1, 'A', 1, Timestamp('2011-01-07 00:00:00'), 15984.24, False],[1, 'C', 2, Timestamp('2010-02-05 00:00:00'), 50605.27, True],[1, 'A', 2, Timestamp('2010-03-05 00:00:00'), 48397.98, False],[1, 'A', 2, Timestamp('2010-04-02 00:00:00'), 47450.5, False],[1, 'A', 2, Timestamp('2010-05-07 00:00:00'), 47903.01, False],[1, 'A', 2, Timestamp('2010-06-04 00:00:00'), 48754.47, False],[1, 'A', 2, Timestamp('2010-07-02 00:00:00'), 47077.72, False],[1, 'A', 2, Timestamp('2010-08-06 00:00:00'), 50031.73, False],[1, 'A', 2, Timestamp('2010-09-03 00:00:00'), 49015.05, False],[1, 'A', 2, Timestamp('2010-10-01 00:00:00'), 45829.02, False],[1, 'A', 2, Timestamp('2010-11-05 00:00:00'), 46381.43, True],[1, 'A', 2, Timestamp('2010-12-03 00:00:00'), 44405.02, False],[1, 'A', 2, Timestamp('2011-01-07 00:00:00'), 43202.29, False],[1, 'A', 3, Timestamp('2010-02-05 00:00:00'), 13740.12, False],[1, 'A', 3, Timestamp('2010-03-05 00:00:00'), 12275.58, False],[1, 'A', 3, Timestamp('2010-04-02 00:00:00'), 11157.08, False],[1, 'A', 3, Timestamp('2010-05-07 00:00:00'), 9372.8, True],[1, 'A', 3, Timestamp('2010-06-04 00:00:00'), 8001.41, False],[1, 'C', 3, Timestamp('2010-07-02 00:00:00'), 7857.88, True],[1, 'A', 3, Timestamp('2010-08-06 00:00:00'), 26719.02, False],[1, 'A', 3, Timestamp('2010-09-03 00:00:00'), 19081.8, False],[1, 'B', 3, Timestamp('2010-10-01 00:00:00'), 9775.17, False],[1, 'A', 3, Timestamp('2010-11-05 00:00:00'), 9825.22, False],[1, 'A', 3, Timestamp('2010-12-03 00:00:00'), 10856.85, False],[1, 'A', 3, Timestamp('2011-01-07 00:00:00'), 15808.15, False],[1, 'A', 4, Timestamp('2010-02-05 00:00:00'), 39954.04, False],[1, 'A', 4, Timestamp('2010-03-05 00:00:00'), 38086.19, False],[1, 'A', 4, Timestamp('2010-04-02 00:00:00'), 37809.49, False],[1, 'A', 4, Timestamp('2010-05-07 00:00:00'), 37168.34, False],[1, 'A', 4, Timestamp('2010-06-04 00:00:00'), 40548.19, False],[1, 'B', 4, Timestamp('2010-07-02 00:00:00'), 39773.71, False],[1, 'A', 4, Timestamp('2010-08-06 00:00:00'), 40973.88, False],[1, 'A', 4, Timestamp('2010-09-03 00:00:00'), 38321.88, False],[1, 'A', 4, Timestamp('2010-10-01 00:00:00'), 34912.45, False],[1, 'A', 4, Timestamp('2010-11-05 00:00:00'), 37980.55, False],[1, 'A', 4, Timestamp('2010-12-03 00:00:00'), 37110.55, False],[1, 'A', 4, Timestamp('2011-01-07 00:00:00'), 37947.8, False],[1, 'A', 5, Timestamp('2010-02-05 00:00:00'), 32229.38, False],[1, 'A', 5, Timestamp('2010-03-05 00:00:00'), 23082.14, False],[1, 'B', 5, Timestamp('2010-04-02 00:00:00'), 29967.92, False],[1, 'A', 5, Timestamp('2010-05-07 00:00:00'), 19260.44, False],[1, 'A', 5, Timestamp('2010-06-04 00:00:00'), 22932.26, False],[1, 'A', 5, Timestamp('2010-07-02 00:00:00'), 18887.71, False],[1, 'A', 5, Timestamp('2010-08-06 00:00:00'), 16926.17, False],[1, 'A', 5, Timestamp('2010-09-03 00:00:00'), 15390.52, False],[1, 'A', 5, Timestamp('2010-10-01 00:00:00'), 23381.38, False],[1, 'A', 5, Timestamp('2010-11-05 00:00:00'), 23903.81, False],[1, 'A', 5, Timestamp('2010-12-03 00:00:00'), 36472.02, False],[1, 'A', 5, Timestamp('2011-01-07 00:00:00'), 22699.69, False],[1, 'A', 6, Timestamp('2010-02-05 00:00:00'), 5749.03, False],[1, 'A', 6, Timestamp('2010-03-05 00:00:00'), 4221.25, False],[1, 'A', 6, Timestamp('2010-04-02 00:00:00'), 4132.61, False],[1, 'A', 6, Timestamp('2010-05-07 00:00:00'), 7477.7, False],[1, 'A', 6, Timestamp('2010-06-04 00:00:00'), 5484.9, False],[1, 'A', 6, Timestamp('2010-07-02 00:00:00'), 4541.91, False],[1, 'A', 6, Timestamp('2010-08-06 00:00:00'), 4700.38, False],[1, 'A', 6, Timestamp('2010-09-03 00:00:00'), 3553.75, False],[1, 'B', 6, Timestamp('2010-10-01 00:00:00'), 2876.19, False],[1, 'A', 6, Timestamp('2010-11-05 00:00:00'), 5036.99, False],[1, 'A', 6, Timestamp('2010-12-03 00:00:00'), 6356.96, False],[1, 'A', 6, Timestamp('2011-01-07 00:00:00'), 1376.15, False],[1, 'A', 7, Timestamp('2010-02-05 00:00:00'), 21084.08, False],[1, 'A', 7, Timestamp('2010-03-05 00:00:00'), 19659.7, False],[1, 'A', 7, Timestamp('2010-04-02 00:00:00'), 22427.62, False],[1, 'A', 7, Timestamp('2010-05-07 00:00:00'), 20457.62, False],[1, 'A', 7, Timestamp('2010-06-04 00:00:00'), 44563.68, False],[1, 'A', 7, Timestamp('2010-07-02 00:00:00'), 22589.0, False],[1, 'A', 7, Timestamp('2010-08-06 00:00:00'), 21842.57, False],[1, 'A', 7, Timestamp('2010-09-03 00:00:00'), 18005.65, False],[1, 'A', 7, Timestamp('2010-10-01 00:00:00'), 16481.79, False],[1, 'A', 7, Timestamp('2010-11-05 00:00:00'), 19136.58, False],[1, 'A', 7, Timestamp('2010-12-03 00:00:00'), 47406.83, False],[1, 'A', 7, Timestamp('2011-01-07 00:00:00'), 17516.16, False],[1, 'A', 8, Timestamp('2010-02-05 00:00:00'), 40129.01, False],[1, 'A', 8, Timestamp('2010-03-05 00:00:00'), 38776.09, False],[1, 'A', 8, Timestamp('2010-04-02 00:00:00'), 38151.58, False],[1, 'A', 8, Timestamp('2010-05-07 00:00:00'), 35393.78, False],[1, 'A', 8, Timestamp('2010-06-04 00:00:00'), 35181.47, False],[1, 'A', 8, Timestamp('2010-07-02 00:00:00'), 35580.01, False],[1, 'A', 8, Timestamp('2010-08-06 00:00:00'), 34833.35, False],[1, 'A', 8, Timestamp('2010-09-03 00:00:00'), 35562.68, False],[1, 'A', 8, Timestamp('2010-10-01 00:00:00'), 34658.25, False],[1, 'A', 8, Timestamp('2010-11-05 00:00:00'), 36182.58, False],[1, 'A', 8, Timestamp('2010-12-03 00:00:00'), 36222.74, False],[1, 'A', 8, Timestamp('2011-01-07 00:00:00'), 36599.46, False],[1, 'A', 9, Timestamp('2010-02-05 00:00:00'), 16930.99, False],[1, 'A', 9, Timestamp('2010-03-05 00:00:00'), 24064.7, False],[1, 'A', 9, Timestamp('2010-04-02 00:00:00'), 25435.02, False],[1, 'A', 9, Timestamp('2010-05-07 00:00:00'), 27588.34, False]])
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
      <td>2747.6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>B</td>
      <td>1</td>
      <td>2010-03-05</td>
      <td>21827.9</td>
      <td>True</td>
      <td>2406.24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>2010-04-02</td>
      <td>57258.4</td>
      <td>False</td>
      <td>6311.98</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>C</td>
      <td>1</td>
      <td>2010-05-07</td>
      <td>17413.9</td>
      <td>False</td>
      <td>1919.66</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>C</td>
      <td>1</td>
      <td>2010-06-04</td>
      <td>17558.1</td>
      <td>False</td>
      <td>1935.55</td>
    </tr>
  </tbody>
</table>
</div>



### `loc[]`
DataFrames can be sliced by index values using `loc[]`
- You can only slice an index if the index is sorted (using .sort_index())
- To slice at the outer level, first and last can be strings
- To slice at inner levels, first and last should be tuples
- If you pass a single slice to .loc[], it will slice the rows


```python
df_srt = df.set_index(['type','department']).sort_index()
```


```python
df_srt.loc['A':'B']
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
      <th></th>
      <th>store</th>
      <th>date</th>
      <th>weekly_sales</th>
      <th>is_holiday</th>
      <th>frac_sales</th>
    </tr>
    <tr>
      <th>type</th>
      <th>department</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">A</th>
      <th>1</th>
      <td>1</td>
      <td>2010-02-05</td>
      <td>24924.5</td>
      <td>False</td>
      <td>2747.6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2010-04-02</td>
      <td>57258.4</td>
      <td>False</td>
      <td>6311.98</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2010-10-01</td>
      <td>20094.2</td>
      <td>True</td>
      <td>2215.12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2011-01-07</td>
      <td>15984.2</td>
      <td>False</td>
      <td>1762.05</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2010-03-05</td>
      <td>48398</td>
      <td>False</td>
      <td>5335.24</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">B</th>
      <th>1</th>
      <td>1</td>
      <td>2010-11-05</td>
      <td>34238.9</td>
      <td>False</td>
      <td>3774.38</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>2010-10-01</td>
      <td>9775.17</td>
      <td>False</td>
      <td>1077.58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>2010-07-02</td>
      <td>39773.7</td>
      <td>False</td>
      <td>4384.53</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>2010-04-02</td>
      <td>29967.9</td>
      <td>False</td>
      <td>3303.57</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1</td>
      <td>2010-10-01</td>
      <td>2876.19</td>
      <td>False</td>
      <td>317.062</td>
    </tr>
  </tbody>
</table>
<p>93 rows × 5 columns</p>
</div>




```python
df_srt.loc[('A',2):('B',1)]
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
      <th></th>
      <th>store</th>
      <th>date</th>
      <th>weekly_sales</th>
      <th>is_holiday</th>
      <th>frac_sales</th>
    </tr>
    <tr>
      <th>type</th>
      <th>department</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="8" valign="top">A</th>
      <th>2</th>
      <td>1</td>
      <td>2010-03-05</td>
      <td>48398</td>
      <td>False</td>
      <td>5335.24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2010-04-02</td>
      <td>47450.5</td>
      <td>False</td>
      <td>5230.79</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2010-05-07</td>
      <td>47903</td>
      <td>False</td>
      <td>5280.67</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2010-06-04</td>
      <td>48754.5</td>
      <td>False</td>
      <td>5374.54</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2010-07-02</td>
      <td>47077.7</td>
      <td>False</td>
      <td>5189.7</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>2010-04-02</td>
      <td>25435</td>
      <td>False</td>
      <td>2803.87</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>2010-05-07</td>
      <td>27588.3</td>
      <td>False</td>
      <td>3041.25</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">B</th>
      <th>1</th>
      <td>1</td>
      <td>2010-03-05</td>
      <td>21827.9</td>
      <td>True</td>
      <td>2406.24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2010-09-03</td>
      <td>16241.8</td>
      <td>False</td>
      <td>1790.44</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2010-11-05</td>
      <td>34238.9</td>
      <td>False</td>
      <td>3774.38</td>
    </tr>
  </tbody>
</table>
<p>85 rows × 5 columns</p>
</div>




```python
df_srt.loc[('A',2):('B',1),['weekly_sales','frac_sales']]
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
      <th></th>
      <th>weekly_sales</th>
      <th>frac_sales</th>
    </tr>
    <tr>
      <th>type</th>
      <th>department</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="8" valign="top">A</th>
      <th>2</th>
      <td>48398</td>
      <td>5335.24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>47450.5</td>
      <td>5230.79</td>
    </tr>
    <tr>
      <th>2</th>
      <td>47903</td>
      <td>5280.67</td>
    </tr>
    <tr>
      <th>2</th>
      <td>48754.5</td>
      <td>5374.54</td>
    </tr>
    <tr>
      <th>2</th>
      <td>47077.7</td>
      <td>5189.7</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>25435</td>
      <td>2803.87</td>
    </tr>
    <tr>
      <th>9</th>
      <td>27588.3</td>
      <td>3041.25</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">B</th>
      <th>1</th>
      <td>21827.9</td>
      <td>2406.24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>16241.8</td>
      <td>1790.44</td>
    </tr>
    <tr>
      <th>1</th>
      <td>34238.9</td>
      <td>3774.38</td>
    </tr>
  </tbody>
</table>
<p>85 rows × 2 columns</p>
</div>




```python
df_srt.loc[('A',2):('B',1),'weekly_sales':'frac_sales']
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
      <th></th>
      <th>weekly_sales</th>
      <th>is_holiday</th>
      <th>frac_sales</th>
    </tr>
    <tr>
      <th>type</th>
      <th>department</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="8" valign="top">A</th>
      <th>2</th>
      <td>48398</td>
      <td>False</td>
      <td>5335.24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>47450.5</td>
      <td>False</td>
      <td>5230.79</td>
    </tr>
    <tr>
      <th>2</th>
      <td>47903</td>
      <td>False</td>
      <td>5280.67</td>
    </tr>
    <tr>
      <th>2</th>
      <td>48754.5</td>
      <td>False</td>
      <td>5374.54</td>
    </tr>
    <tr>
      <th>2</th>
      <td>47077.7</td>
      <td>False</td>
      <td>5189.7</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>25435</td>
      <td>False</td>
      <td>2803.87</td>
    </tr>
    <tr>
      <th>9</th>
      <td>27588.3</td>
      <td>False</td>
      <td>3041.25</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">B</th>
      <th>1</th>
      <td>21827.9</td>
      <td>True</td>
      <td>2406.24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>16241.8</td>
      <td>False</td>
      <td>1790.44</td>
    </tr>
    <tr>
      <th>1</th>
      <td>34238.9</td>
      <td>False</td>
      <td>3774.38</td>
    </tr>
  </tbody>
</table>
<p>85 rows × 3 columns</p>
</div>



### `iloc[]`


```python
df.iloc[:5,2:3]
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
      <th>department</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>


