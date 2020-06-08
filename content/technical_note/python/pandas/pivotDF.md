---
title: "DataFrames pivot tables"
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
      <td>13457.3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>B</td>
      <td>1</td>
      <td>2010-03-05</td>
      <td>21827.9</td>
      <td>True</td>
      <td>11785.3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>2010-04-02</td>
      <td>57258.4</td>
      <td>False</td>
      <td>30915</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>C</td>
      <td>1</td>
      <td>2010-05-07</td>
      <td>17413.9</td>
      <td>False</td>
      <td>9402.16</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>C</td>
      <td>1</td>
      <td>2010-06-04</td>
      <td>17558.1</td>
      <td>False</td>
      <td>9479.98</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby(['type','is_holiday'])[['weekly_sales','frac_sales']].agg([np.min,np.max])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th colspan="2" halign="left">weekly_sales</th>
      <th colspan="2" halign="left">frac_sales</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>amin</th>
      <th>amax</th>
      <th>amin</th>
      <th>amax</th>
    </tr>
    <tr>
      <th>type</th>
      <th>is_holiday</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">A</th>
      <th>False</th>
      <td>1376.15</td>
      <td>57258.43</td>
      <td>743.012533</td>
      <td>30915.039145</td>
    </tr>
    <tr>
      <th>True</th>
      <td>9372.80</td>
      <td>46381.43</td>
      <td>5060.573245</td>
      <td>25042.316460</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">B</th>
      <th>False</th>
      <td>2876.19</td>
      <td>39773.71</td>
      <td>1552.915901</td>
      <td>21474.668474</td>
    </tr>
    <tr>
      <th>True</th>
      <td>21827.90</td>
      <td>21827.90</td>
      <td>11785.345546</td>
      <td>11785.345546</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">C</th>
      <th>False</th>
      <td>16333.14</td>
      <td>22517.56</td>
      <td>8818.608237</td>
      <td>12157.707587</td>
    </tr>
    <tr>
      <th>True</th>
      <td>7857.88</td>
      <td>50605.27</td>
      <td>4242.635849</td>
      <td>27322.857141</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.pivot_table(values=['weekly_sales','frac_sales'], index=['type','is_holiday'],aggfunc=[np.min,np.max])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th colspan="2" halign="left">amin</th>
      <th colspan="2" halign="left">amax</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>frac_sales</th>
      <th>weekly_sales</th>
      <th>frac_sales</th>
      <th>weekly_sales</th>
    </tr>
    <tr>
      <th>type</th>
      <th>is_holiday</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">A</th>
      <th>False</th>
      <td>743.012533</td>
      <td>1376.15</td>
      <td>30915.039145</td>
      <td>57258.43</td>
    </tr>
    <tr>
      <th>True</th>
      <td>5060.573245</td>
      <td>9372.80</td>
      <td>25042.316460</td>
      <td>46381.43</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">B</th>
      <th>False</th>
      <td>1552.915901</td>
      <td>2876.19</td>
      <td>21474.668474</td>
      <td>39773.71</td>
    </tr>
    <tr>
      <th>True</th>
      <td>11785.345546</td>
      <td>21827.90</td>
      <td>11785.345546</td>
      <td>21827.90</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">C</th>
      <th>False</th>
      <td>8818.608237</td>
      <td>16333.14</td>
      <td>12157.707587</td>
      <td>22517.56</td>
    </tr>
    <tr>
      <th>True</th>
      <td>4242.635849</td>
      <td>7857.88</td>
      <td>27322.857141</td>
      <td>50605.27</td>
    </tr>
  </tbody>
</table>
</div>



#### Add margins


```python
df.pivot_table(values=['weekly_sales','frac_sales'], index=['type','is_holiday'],aggfunc=[np.min,np.max], margins=True)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th colspan="2" halign="left">amin</th>
      <th colspan="2" halign="left">amax</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>frac_sales</th>
      <th>weekly_sales</th>
      <th>frac_sales</th>
      <th>weekly_sales</th>
    </tr>
    <tr>
      <th>type</th>
      <th>is_holiday</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">A</th>
      <th>False</th>
      <td>743.012533</td>
      <td>1376.15</td>
      <td>30915.039145</td>
      <td>57258.43</td>
    </tr>
    <tr>
      <th>True</th>
      <td>5060.573245</td>
      <td>9372.80</td>
      <td>25042.316460</td>
      <td>46381.43</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">B</th>
      <th>False</th>
      <td>1552.915901</td>
      <td>2876.19</td>
      <td>21474.668474</td>
      <td>39773.71</td>
    </tr>
    <tr>
      <th>True</th>
      <td>11785.345546</td>
      <td>21827.90</td>
      <td>11785.345546</td>
      <td>21827.90</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">C</th>
      <th>False</th>
      <td>8818.608237</td>
      <td>16333.14</td>
      <td>12157.707587</td>
      <td>22517.56</td>
    </tr>
    <tr>
      <th>True</th>
      <td>4242.635849</td>
      <td>7857.88</td>
      <td>27322.857141</td>
      <td>50605.27</td>
    </tr>
    <tr>
      <th>All</th>
      <th></th>
      <td>743.012533</td>
      <td>1376.15</td>
      <td>30915.039145</td>
      <td>57258.43</td>
    </tr>
  </tbody>
</table>
</div>



### Adding a column


```python
df.pivot_table(values='weekly_sales', index='type', columns='is_holiday', aggfunc=np.max)
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
      <th>is_holiday</th>
      <th>False</th>
      <th>True</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>57258.43</td>
      <td>46381.43</td>
    </tr>
    <tr>
      <th>B</th>
      <td>39773.71</td>
      <td>21827.90</td>
    </tr>
    <tr>
      <th>C</th>
      <td>22517.56</td>
      <td>50605.27</td>
    </tr>
  </tbody>
</table>
</div>



### Fill missing with 0


```python
df.pivot_table(values='weekly_sales', index='type', columns='is_holiday', aggfunc=np.max, fill_value=0)
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
      <th>is_holiday</th>
      <th>False</th>
      <th>True</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>57258.43</td>
      <td>46381.43</td>
    </tr>
    <tr>
      <th>B</th>
      <td>39773.71</td>
      <td>21827.90</td>
    </tr>
    <tr>
      <th>C</th>
      <td>22517.56</td>
      <td>50605.27</td>
    </tr>
  </tbody>
</table>
</div>



### Working with pivot tables


```python
df['year'] = df['date'].dt.year
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
      <th>year</th>
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
      <td>220.866</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>B</td>
      <td>1</td>
      <td>2010-03-05</td>
      <td>21827.9</td>
      <td>True</td>
      <td>193.426</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>2010-04-02</td>
      <td>57258.4</td>
      <td>False</td>
      <td>507.39</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>C</td>
      <td>1</td>
      <td>2010-05-07</td>
      <td>17413.9</td>
      <td>False</td>
      <td>154.312</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>C</td>
      <td>1</td>
      <td>2010-06-04</td>
      <td>17558.1</td>
      <td>False</td>
      <td>155.589</td>
      <td>2010</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_by_type_vs_year = df.pivot_table(values='weekly_sales', index=['type','is_holiday'], columns='year',aggfunc=np.min)
```


```python
# Get the worldwide mean temp by year
mean_temp_by_year = df_by_type_vs_year.mean()
# Filter for the year that had the highest mean temp
print(mean_temp_by_year[mean_temp_by_year==mean_temp_by_year.max()])
```

    year
    2010    10303.61
    dtype: float64



```python
# Get the mean temp by city
mean_temp_by_city = df_by_type_vs_year.mean(axis='columns')
# Filter for the city that had the lowest mean temp
print(mean_temp_by_city[mean_temp_by_city==mean_temp_by_city.min()])
```

    type  is_holiday
    A     False         2464.95
    dtype: float64

