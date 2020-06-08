---
title: "DataFrames basics"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### DataFrames
store tabular data where you can label the rows and the columns.

#### DataFrame from dictionary


```python
import pandas as pd

# Build cars DataFrame
names = ['United States', 'Australia', 'Japan', 'India', 'Russia', 'Morocco', 'Egypt']
dr =  [True, False, False, False, True, True, True]
cpc = [809, 731, 588, 18, 200, 70, 45]
cars_dict = { 'country':names, 'drives_right':dr, 'cars_per_cap':cpc }
cars = pd.DataFrame(cars_dict)
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


#### Set the row attribute


```python
# Definition of row_labels
row_labels = ['US', 'AUS', 'JPN', 'IN', 'RU', 'MOR', 'EG']

# Specify row labels of cars
cars.index = row_labels
```

               country  drives_right  cars_per_cap
    US   United States          True           809
    AUS      Australia         False           731
    JPN          Japan         False           588
    IN           India         False            18
    RU          Russia          True           200
    MOR        Morocco          True            70
    EG           Egypt          True            45


### Useful exploration
#### Methods
- `.head()` first few rows
- `.info()` name of columns, data type and number of missing values...
- `.describe()` summary statistics

#### Attributes
- `.shape` attribute for rows x columns
- `.values` converts to a 2D numpy array
- `.columns` An index of columns: the column names.
- `.index` An index for the rows: either row numbers or row names


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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>United States</td>
      <td>True</td>
      <td>809</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Australia</td>
      <td>False</td>
      <td>731</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Japan</td>
      <td>False</td>
      <td>588</td>
    </tr>
    <tr>
      <th>3</th>
      <td>India</td>
      <td>False</td>
      <td>18</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Russia</td>
      <td>True</td>
      <td>200</td>
    </tr>
  </tbody>
</table>
</div>




```python
cars.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 7 entries, 0 to 6
    Data columns (total 3 columns):
     #   Column        Non-Null Count  Dtype 
    ---  ------        --------------  ----- 
     0   country       7 non-null      object
     1   drives_right  7 non-null      bool  
     2   cars_per_cap  7 non-null      int64 
    dtypes: bool(1), int64(1), object(1)
    memory usage: 175.0+ bytes



```python
cars.shape
```




    (7, 3)




```python
cars.describe()
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
      <th>count</th>
      <td>7.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>351.571429</td>
    </tr>
    <tr>
      <th>std</th>
      <td>345.595552</td>
    </tr>
    <tr>
      <th>min</th>
      <td>18.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>57.500000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>200.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>659.500000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>809.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
cars.values
```




    array([['United States', True, 809],
           ['Australia', False, 731],
           ['Japan', False, 588],
           ['India', False, 18],
           ['Russia', True, 200],
           ['Morocco', True, 70],
           ['Egypt', True, 45]], dtype=object)




```python
cars.columns
```




    Index(['country', 'drives_right', 'cars_per_cap'], dtype='object')




```python
cars.index
```




    Int64Index([0, 1, 2, 3, 4, 5, 6], dtype='int64')



### Save to csv


```python
# Print cars again
print(cars)
cars.to_csv('cars.csv',index=True)
```

             country  drives_right  cars_per_cap
    0  United States          True           809
    1      Australia         False           731
    2          Japan         False           588
    3          India         False            18
    4         Russia          True           200
    5        Morocco          True            70
    6          Egypt          True            45


#### Read csv


```python
# Import pandas as pd
import pandas as pd

# Import the cars.csv data: cars
cars = pd.read_csv('cars.csv')

# Print out cars
print(cars)
```

       Unnamed: 0        country  drives_right  cars_per_cap
    0           0  United States          True           809
    1           1      Australia         False           731
    2           2          Japan         False           588
    3           3          India         False            18
    4           4         Russia          True           200
    5           5        Morocco          True            70
    6           6          Egypt          True            45



```python
#Fix import by including index_col
cars = pd.read_csv('cars.csv',index_col=0)

# Print out cars
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

