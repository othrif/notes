---
title: "Sort DataFrames"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Most common types of data manipulation: 
- sorting rows
- subsetting columns
- subsetting rows
- adding new columns

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


### Sorting row


```python
cars.sort_values('cars_per_cap')
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
      <th>IN</th>
      <td>India</td>
      <td>False</td>
      <td>18</td>
    </tr>
    <tr>
      <th>EG</th>
      <td>Egypt</td>
      <td>True</td>
      <td>45</td>
    </tr>
    <tr>
      <th>MOR</th>
      <td>Morocco</td>
      <td>True</td>
      <td>70</td>
    </tr>
    <tr>
      <th>RU</th>
      <td>Russia</td>
      <td>True</td>
      <td>200</td>
    </tr>
    <tr>
      <th>JPN</th>
      <td>Japan</td>
      <td>False</td>
      <td>588</td>
    </tr>
    <tr>
      <th>AUS</th>
      <td>Australia</td>
      <td>False</td>
      <td>731</td>
    </tr>
    <tr>
      <th>US</th>
      <td>United States</td>
      <td>True</td>
      <td>809</td>
    </tr>
  </tbody>
</table>
</div>




```python
cars.sort_values(['drives_right','cars_per_cap'], ascending=[True,False])
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
    <tr>
      <th>IN</th>
      <td>India</td>
      <td>False</td>
      <td>18</td>
    </tr>
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



### subsetting columns


```python
cars['country'].head()
```




    US     United States
    AUS        Australia
    JPN            Japan
    IN             India
    RU            Russia
    Name: country, dtype: object




```python
cars[['country','cars_per_cap']].head()
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
      <th>cars_per_cap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>US</th>
      <td>United States</td>
      <td>809</td>
    </tr>
    <tr>
      <th>AUS</th>
      <td>Australia</td>
      <td>731</td>
    </tr>
    <tr>
      <th>JPN</th>
      <td>Japan</td>
      <td>588</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>India</td>
      <td>18</td>
    </tr>
    <tr>
      <th>RU</th>
      <td>Russia</td>
      <td>200</td>
    </tr>
  </tbody>
</table>
</div>



### subsetting rows


```python
cars[cars['cars_per_cap']<100].head()
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
      <th>IN</th>
      <td>India</td>
      <td>False</td>
      <td>18</td>
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



#### Subsetting by categorical variables
- `.isin()` one condition instead of several `or`, `|`


```python
cars[cars['country'].isin(['Morocco','Egypt'])]
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



### adding new columns


```python
cars['cars_per_cap_10'] = cars['cars_per_cap']*10
```


```python
cars.head()
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
      <th>cars_per_cap_10</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>US</th>
      <td>United States</td>
      <td>True</td>
      <td>809</td>
      <td>8090</td>
    </tr>
    <tr>
      <th>AUS</th>
      <td>Australia</td>
      <td>False</td>
      <td>731</td>
      <td>7310</td>
    </tr>
    <tr>
      <th>JPN</th>
      <td>Japan</td>
      <td>False</td>
      <td>588</td>
      <td>5880</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>India</td>
      <td>False</td>
      <td>18</td>
      <td>180</td>
    </tr>
    <tr>
      <th>RU</th>
      <td>Russia</td>
      <td>True</td>
      <td>200</td>
      <td>2000</td>
    </tr>
  </tbody>
</table>
</div>


