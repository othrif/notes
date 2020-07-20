---
title: "Using merge_ordered() and merge_asof() to merge DataFrames"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### merge_ordered()
default = outer merge


```python
import pandas as pd

austin = pd.read_csv('austin.csv', delim_whitespace=True)
houston = pd.read_csv('houston.csv', delim_whitespace=True)
```


```python
# Perform the first ordered merge: tx_weather
tx_weather = pd.merge_ordered(austin,houston)
tx_weather
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
      <th>date</th>
      <th>ratings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016-01-01</td>
      <td>Cloudy</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-01-04</td>
      <td>Rainy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-01-17</td>
      <td>Sunny</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-02-08</td>
      <td>Cloudy</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016-03-01</td>
      <td>Sunny</td>
    </tr>
  </tbody>
</table>
</div>



All information about the city is lost


```python
# Perform the second ordered merge: tx_weather_suff
tx_weather_suff = pd.merge_ordered(austin,houston, on ='date', suffixes=['_aus', '_hus'])
tx_weather_suff
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
      <th>date</th>
      <th>ratings_aus</th>
      <th>ratings_hus</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016-01-01</td>
      <td>Cloudy</td>
      <td>Cloudy</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-01-04</td>
      <td>NaN</td>
      <td>Rainy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-01-17</td>
      <td>Sunny</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-02-08</td>
      <td>Cloudy</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016-03-01</td>
      <td>NaN</td>
      <td>Sunny</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Perform the third ordered merge: tx_weather_ffill
tx_weather_ffill = pd.merge_ordered(austin,houston, on='date', suffixes=['_aus', '_hus'], fill_method='ffill')
tx_weather_ffill
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
      <th>date</th>
      <th>ratings_aus</th>
      <th>ratings_hus</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016-01-01</td>
      <td>Cloudy</td>
      <td>Cloudy</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-01-04</td>
      <td>Cloudy</td>
      <td>Rainy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-01-17</td>
      <td>Sunny</td>
      <td>Rainy</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-02-08</td>
      <td>Cloudy</td>
      <td>Rainy</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016-03-01</td>
      <td>Cloudy</td>
      <td>Sunny</td>
    </tr>
  </tbody>
</table>
</div>



###  merge_asof()
Similar to `pd.merge_ordered()`, the `pd.merge_asof()` function will also merge values in order using the on column, but for each row in the left DataFrame, **only rows from the right DataFrame whose 'on' column values are less than the left value will be kept**.


```python
import pandas as pd

auto = pd.read_csv('automobiles.csv', parse_dates=['yr'])
oil = pd.read_csv('oil_price.csv', parse_dates=['Date'])
```


```python
auto.head()
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
      <th>mpg</th>
      <th>cyl</th>
      <th>displ</th>
      <th>hp</th>
      <th>weight</th>
      <th>accel</th>
      <th>yr</th>
      <th>origin</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>18.0</td>
      <td>8</td>
      <td>307.0</td>
      <td>130</td>
      <td>3504</td>
      <td>12.0</td>
      <td>1970-01-01</td>
      <td>US</td>
      <td>chevrolet chevelle malibu</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15.0</td>
      <td>8</td>
      <td>350.0</td>
      <td>165</td>
      <td>3693</td>
      <td>11.5</td>
      <td>1970-01-01</td>
      <td>US</td>
      <td>buick skylark 320</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18.0</td>
      <td>8</td>
      <td>318.0</td>
      <td>150</td>
      <td>3436</td>
      <td>11.0</td>
      <td>1970-01-01</td>
      <td>US</td>
      <td>plymouth satellite</td>
    </tr>
    <tr>
      <th>3</th>
      <td>16.0</td>
      <td>8</td>
      <td>304.0</td>
      <td>150</td>
      <td>3433</td>
      <td>12.0</td>
      <td>1970-01-01</td>
      <td>US</td>
      <td>amc rebel sst</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17.0</td>
      <td>8</td>
      <td>302.0</td>
      <td>140</td>
      <td>3449</td>
      <td>10.5</td>
      <td>1970-01-01</td>
      <td>US</td>
      <td>ford torino</td>
    </tr>
  </tbody>
</table>
</div>




```python
oil.head()
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
      <th>Date</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1970-01-01</td>
      <td>3.35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1970-02-01</td>
      <td>3.35</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1970-03-01</td>
      <td>3.35</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1970-04-01</td>
      <td>3.35</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1970-05-01</td>
      <td>3.35</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merge auto and oil: merged
merged = pd.merge_asof(auto, oil, left_on='yr', right_on='Date')
merged.tail()
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
      <th>mpg</th>
      <th>cyl</th>
      <th>displ</th>
      <th>hp</th>
      <th>weight</th>
      <th>accel</th>
      <th>yr</th>
      <th>origin</th>
      <th>name</th>
      <th>Date</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>387</th>
      <td>27.0</td>
      <td>4</td>
      <td>140.0</td>
      <td>86</td>
      <td>2790</td>
      <td>15.6</td>
      <td>1982-01-01</td>
      <td>US</td>
      <td>ford mustang gl</td>
      <td>1982-01-01</td>
      <td>33.85</td>
    </tr>
    <tr>
      <th>388</th>
      <td>44.0</td>
      <td>4</td>
      <td>97.0</td>
      <td>52</td>
      <td>2130</td>
      <td>24.6</td>
      <td>1982-01-01</td>
      <td>Europe</td>
      <td>vw pickup</td>
      <td>1982-01-01</td>
      <td>33.85</td>
    </tr>
    <tr>
      <th>389</th>
      <td>32.0</td>
      <td>4</td>
      <td>135.0</td>
      <td>84</td>
      <td>2295</td>
      <td>11.6</td>
      <td>1982-01-01</td>
      <td>US</td>
      <td>dodge rampage</td>
      <td>1982-01-01</td>
      <td>33.85</td>
    </tr>
    <tr>
      <th>390</th>
      <td>28.0</td>
      <td>4</td>
      <td>120.0</td>
      <td>79</td>
      <td>2625</td>
      <td>18.6</td>
      <td>1982-01-01</td>
      <td>US</td>
      <td>ford ranger</td>
      <td>1982-01-01</td>
      <td>33.85</td>
    </tr>
    <tr>
      <th>391</th>
      <td>31.0</td>
      <td>4</td>
      <td>119.0</td>
      <td>82</td>
      <td>2720</td>
      <td>19.4</td>
      <td>1982-01-01</td>
      <td>US</td>
      <td>chevy s-10</td>
      <td>1982-01-01</td>
      <td>33.85</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Resample merged: yearly
yearly = merged.resample('A', on='Date')[['mpg','Price']].mean()
yearly
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
      <th>mpg</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1970-12-31</th>
      <td>17.689655</td>
      <td>3.35</td>
    </tr>
    <tr>
      <th>1971-12-31</th>
      <td>21.111111</td>
      <td>3.56</td>
    </tr>
    <tr>
      <th>1972-12-31</th>
      <td>18.714286</td>
      <td>3.56</td>
    </tr>
    <tr>
      <th>1973-12-31</th>
      <td>17.100000</td>
      <td>3.56</td>
    </tr>
    <tr>
      <th>1974-12-31</th>
      <td>22.769231</td>
      <td>10.11</td>
    </tr>
    <tr>
      <th>1975-12-31</th>
      <td>20.266667</td>
      <td>11.16</td>
    </tr>
    <tr>
      <th>1976-12-31</th>
      <td>21.573529</td>
      <td>11.16</td>
    </tr>
    <tr>
      <th>1977-12-31</th>
      <td>23.375000</td>
      <td>13.90</td>
    </tr>
    <tr>
      <th>1978-12-31</th>
      <td>24.061111</td>
      <td>14.85</td>
    </tr>
    <tr>
      <th>1979-12-31</th>
      <td>25.093103</td>
      <td>14.85</td>
    </tr>
    <tr>
      <th>1980-12-31</th>
      <td>33.803704</td>
      <td>32.50</td>
    </tr>
    <tr>
      <th>1981-12-31</th>
      <td>30.185714</td>
      <td>38.00</td>
    </tr>
    <tr>
      <th>1982-12-31</th>
      <td>32.000000</td>
      <td>33.85</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Pearson correlation between the resampled 'Price' and 'mpg'
yearly.corr()
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
      <th>mpg</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>mpg</th>
      <td>1.000000</td>
      <td>0.948677</td>
    </tr>
    <tr>
      <th>Price</th>
      <td>0.948677</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>



It looks like there is a strong correlation between miles per gallon and the price of oil!!
