---
title: "Indexing and selecting DataFrames"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### DataFrames
store tabular data where you can label the rows and the columns.

#### Generate some data


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


### Square brackets
The single bracket version gives a Pandas Series, the double bracket version gives a Pandas DataFrame.

#### Columns


```python
# Print out country column as Pandas Series
cars['country']
```




    US     United States
    AUS        Australia
    JPN            Japan
    IN             India
    RU            Russia
    MOR          Morocco
    EG             Egypt
    Name: country, dtype: object




```python
# Print out country column as Pandas DataFrame
cars[['country']]
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>US</th>
      <td>United States</td>
    </tr>
    <tr>
      <th>AUS</th>
      <td>Australia</td>
    </tr>
    <tr>
      <th>JPN</th>
      <td>Japan</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>India</td>
    </tr>
    <tr>
      <th>RU</th>
      <td>Russia</td>
    </tr>
    <tr>
      <th>MOR</th>
      <td>Morocco</td>
    </tr>
    <tr>
      <th>EG</th>
      <td>Egypt</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Print out DataFrame with country and drives_right columns
cars[['country','drives_right']]
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>US</th>
      <td>United States</td>
      <td>True</td>
    </tr>
    <tr>
      <th>AUS</th>
      <td>Australia</td>
      <td>False</td>
    </tr>
    <tr>
      <th>JPN</th>
      <td>Japan</td>
      <td>False</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>India</td>
      <td>False</td>
    </tr>
    <tr>
      <th>RU</th>
      <td>Russia</td>
      <td>True</td>
    </tr>
    <tr>
      <th>MOR</th>
      <td>Morocco</td>
      <td>True</td>
    </tr>
    <tr>
      <th>EG</th>
      <td>Egypt</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



#### Rows


```python
# Print out first 3 observations
cars[0:3]
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
      <th>AUS</th>
      <td>Australia</td>
      <td>False</td>
      <td>731</td>
    </tr>
    <tr>
      <th>JPN</th>
      <td>Japan</td>
      <td>False</td>
      <td>588</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Print out fourth, fifth and sixth observation
print(cars[3:6])
```

         country  drives_right  cars_per_cap
    IN     India         False            18
    RU    Russia          True           200
    MOR  Morocco          True            70


### Selecting rows and columns with `loc` and `iloc`
`loc` is label-based, which means that you have to specify rows and columns based on their row and column labels   
`iloc` is integer index based, so you have to specify rows and columns by their integer index like you did in the previous exercise


```python
# Selecting rows based on index column
# One bracket -> Series
cars.loc['RU']
```




    country         Russia
    drives_right      True
    cars_per_cap       200
    Name: RU, dtype: object




```python
cars.iloc[4]
```




    country         Russia
    drives_right      True
    cars_per_cap       200
    Name: RU, dtype: object




```python
# Two bracket -> DataFrame
cars.loc[['RU']]
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
      <th>RU</th>
      <td>Russia</td>
      <td>True</td>
      <td>200</td>
    </tr>
  </tbody>
</table>
</div>




```python
cars.loc[['RU', 'AUS']]
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
      <th>RU</th>
      <td>Russia</td>
      <td>True</td>
      <td>200</td>
    </tr>
    <tr>
      <th>AUS</th>
      <td>Australia</td>
      <td>False</td>
      <td>731</td>
    </tr>
  </tbody>
</table>
</div>




```python
cars.loc[:,['drives_right']]
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
      <th>drives_right</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>US</th>
      <td>True</td>
    </tr>
    <tr>
      <th>AUS</th>
      <td>False</td>
    </tr>
    <tr>
      <th>JPN</th>
      <td>False</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>False</td>
    </tr>
    <tr>
      <th>RU</th>
      <td>True</td>
    </tr>
    <tr>
      <th>MOR</th>
      <td>True</td>
    </tr>
    <tr>
      <th>EG</th>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
cars.loc[['US', 'MOR'],['drives_right']]
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
      <th>drives_right</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>US</th>
      <td>True</td>
    </tr>
    <tr>
      <th>MOR</th>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
cars.iloc[0:6,[2]]
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
      <th>cars_per_cap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>US</th>
      <td>809</td>
    </tr>
    <tr>
      <th>AUS</th>
      <td>731</td>
    </tr>
    <tr>
      <th>JPN</th>
      <td>588</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>18</td>
    </tr>
    <tr>
      <th>RU</th>
      <td>200</td>
    </tr>
    <tr>
      <th>MOR</th>
      <td>70</td>
    </tr>
  </tbody>
</table>
</div>




```python
cars.loc['US':'MOR',['cars_per_cap']]
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
      <th>cars_per_cap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>US</th>
      <td>809</td>
    </tr>
    <tr>
      <th>AUS</th>
      <td>731</td>
    </tr>
    <tr>
      <th>JPN</th>
      <td>588</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>18</td>
    </tr>
    <tr>
      <th>RU</th>
      <td>200</td>
    </tr>
    <tr>
      <th>MOR</th>
      <td>70</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
