---
title: "Create DataFrame with multiindexes and concatenate with keys"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import pandas as pd
bronze = {'Country':{'United States':  1052.0,
       'Soviet Union':   584.0,
       'United Kingdom':   505.0,
       'France':   475.0,
       'Germany':   454.0}}
silver ={'Country':{
       'United States':  1195.0,
       'Soviet Union':   627.0,
       'United Kingdom':   591.0,
       'France':   461.0,
       'Italy':   394.0}}
gold   = {'Country':{
       'United States':  2088.0,
       'Soviet Union':   838.0,
       'United Kingdom':   498.0,
       'Italy':   460.0,
       'Germany':   407.0}}

medal_types = ['bronze','silver','gold']
medals_all = [ pd.DataFrame(i) for i in [bronze,silver,gold]]
medals = pd.concat(medals_all, keys=medal_types)
medals
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
      <th>Country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">bronze</th>
      <th>France</th>
      <td>475.0</td>
    </tr>
    <tr>
      <th>Germany</th>
      <td>454.0</td>
    </tr>
    <tr>
      <th>Soviet Union</th>
      <td>584.0</td>
    </tr>
    <tr>
      <th>United Kingdom</th>
      <td>505.0</td>
    </tr>
    <tr>
      <th>United States</th>
      <td>1052.0</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">silver</th>
      <th>France</th>
      <td>461.0</td>
    </tr>
    <tr>
      <th>Italy</th>
      <td>394.0</td>
    </tr>
    <tr>
      <th>Soviet Union</th>
      <td>627.0</td>
    </tr>
    <tr>
      <th>United Kingdom</th>
      <td>591.0</td>
    </tr>
    <tr>
      <th>United States</th>
      <td>1195.0</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">gold</th>
      <th>Germany</th>
      <td>407.0</td>
    </tr>
    <tr>
      <th>Italy</th>
      <td>460.0</td>
    </tr>
    <tr>
      <th>Soviet Union</th>
      <td>838.0</td>
    </tr>
    <tr>
      <th>United Kingdom</th>
      <td>498.0</td>
    </tr>
    <tr>
      <th>United States</th>
      <td>2088.0</td>
    </tr>
  </tbody>
</table>
</div>



### Concatenating vertically to get MultiIndexed rows



```python
# Sort the entries of medals: medals_sorted
medals_sorted = medals.sort_index(level=0)

# Print the number of Bronze medals won by Germany
print(medals_sorted.loc[('bronze','Germany')])
```

    Country    454.0
    Name: (bronze, Germany), dtype: float64



```python
# Print data about silver medals
print(medals_sorted.loc['silver'])
```

                    Country
    France            461.0
    Italy             394.0
    Soviet Union      627.0
    United Kingdom    591.0
    United States    1195.0



```python

# Create alias for pd.IndexSlice: idx
idx = pd.IndexSlice

# Print all the data on medals won by the United Kingdom
print(medals_sorted.loc[idx[:,'United Kingdom'],:])

```

                           Country
    bronze United Kingdom    505.0
    gold   United Kingdom    498.0
    silver United Kingdom    591.0


### Concatenating horizontally to get MultiIndexed columns


```python
import pandas as pd

names = ['Hardware', 'Software', 'Service']

dataframes=[]
for name in names:
    filename = 'Sales/feb-sales-%s.csv' % name
    dataframe=pd.read_csv(filename, index_col=0, parse_dates=True)
    dataframes.append(dataframe)
print(dataframes)
```

    [                             Company   Product  Units
    Date                                                 
    2015-02-04 21:52:45  Acme Coporation  Hardware     14
    2015-02-07 22:58:10  Acme Coporation  Hardware      1
    2015-02-19 10:59:33        Mediacore  Hardware     16
    2015-02-02 20:54:49        Mediacore  Hardware      9
    2015-02-21 20:41:47            Hooli  Hardware      3,                              Company   Product  Units
    Date                                                 
    2015-02-16 12:09:19            Hooli  Software     10
    2015-02-03 14:14:18          Initech  Software     13
    2015-02-02 08:33:01            Hooli  Software      3
    2015-02-05 01:53:06  Acme Coporation  Software     19
    2015-02-11 20:03:08          Initech  Software      7
    2015-02-09 13:09:55        Mediacore  Software      7
    2015-02-11 22:50:44            Hooli  Software      4
    2015-02-04 15:36:29        Streeplex  Software     13
    2015-02-21 05:01:26        Mediacore  Software      3,                        Company  Product  Units
    Date                                          
    2015-02-26 08:57:45  Streeplex  Service      4
    2015-02-25 00:29:00    Initech  Service     10
    2015-02-09 08:57:30  Streeplex  Service     19
    2015-02-26 08:58:51  Streeplex  Service      1
    2015-02-05 22:05:03      Hooli  Service     10
    2015-02-19 16:02:58  Mediacore  Service     10]



```python
# Concatenate dataframes: february
february = pd.concat(dataframes, axis=1, keys=['Hardware', 'Software', 'Service'])

# Print february.info()
print(february.info())

# Assign pd.IndexSlice: idx
idx = pd.IndexSlice

# Create the slice: slice_2_8
slice_2_8 = february.loc['Feb. 2, 2015':' Feb. 8, 2015', idx[:, 'Company']]

# Print slice_2_8
print(slice_2_8)
```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 20 entries, 2015-02-02 08:33:01 to 2015-02-26 08:58:51
    Data columns (total 9 columns):
     #   Column               Non-Null Count  Dtype  
    ---  ------               --------------  -----  
     0   (Hardware, Company)  5 non-null      object 
     1   (Hardware, Product)  5 non-null      object 
     2   (Hardware, Units)    5 non-null      float64
     3   (Software, Company)  9 non-null      object 
     4   (Software, Product)  9 non-null      object 
     5   (Software, Units)    9 non-null      float64
     6   (Service, Company)   6 non-null      object 
     7   (Service, Product)   6 non-null      object 
     8   (Service, Units)     6 non-null      float64
    dtypes: float64(3), object(6)
    memory usage: 1.6+ KB
    None
                                Hardware         Software Service
                                 Company          Company Company
    Date                                                         
    2015-02-02 08:33:01              NaN            Hooli     NaN
    2015-02-02 20:54:49        Mediacore              NaN     NaN
    2015-02-03 14:14:18              NaN          Initech     NaN
    2015-02-04 15:36:29              NaN        Streeplex     NaN
    2015-02-04 21:52:45  Acme Coporation              NaN     NaN
    2015-02-05 01:53:06              NaN  Acme Coporation     NaN
    2015-02-05 22:05:03              NaN              NaN   Hooli
    2015-02-07 22:58:10  Acme Coporation              NaN     NaN



```python
# Make the list of tuples: month_list
month_list = [('january', jan), ('february', feb), ('march', mar)]

# Create an empty dictionary: month_dict
month_dict = {}

for month_name, month_data in month_list:

    # Group month_data: month_dict[month_name]
    month_dict[month_name] = month_data.groupby('Company').sum()

# Concatenate data in month_dict: sales
sales = pd.concat(month_dict)

# Print sales
print(sales)

# Print all sales by Mediacore
idx = pd.IndexSlice
print(sales.loc[idx[:, 'Mediacore'], :])
```

                              Units
             Company               
    january  Acme Coporation     76
             Hooli               70
             Initech             37
             Mediacore           15
             Streeplex           50
    february Acme Coporation     34
             Hooli               30
             Initech             30
             Mediacore           45
             Streeplex           37
    march    Acme Coporation      5
             Hooli               37
             Initech             68
             Mediacore           68
             Streeplex           40
                        Units
             Company         
    january  Mediacore     15
    february Mediacore     45
    march    Mediacore     68

