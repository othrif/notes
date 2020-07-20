---
title: "Merging DataFrames with merge() and join()"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Merging with specific columns


```python
import pandas as pd

gold = pd.read_csv('SummerOlympic/Gold.csv')
bronze = pd.read_csv('SummerOlympic/Bronze.csv')
```


```python
gold.head()
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
      <th>NOC</th>
      <th>Country</th>
      <th>Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>USA</td>
      <td>United States</td>
      <td>2088.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>URS</td>
      <td>Soviet Union</td>
      <td>838.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GBR</td>
      <td>United Kingdom</td>
      <td>498.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>FRA</td>
      <td>France</td>
      <td>378.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GER</td>
      <td>Germany</td>
      <td>407.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
bronze.head()
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
      <th>NOC</th>
      <th>Country</th>
      <th>Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>USA</td>
      <td>United States</td>
      <td>1052.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>URS</td>
      <td>Soviet Union</td>
      <td>584.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GBR</td>
      <td>United Kingdom</td>
      <td>505.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>FRA</td>
      <td>France</td>
      <td>475.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GER</td>
      <td>Germany</td>
      <td>454.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
combine = pd.merge(gold, bronze, on=['NOC','Country'], suffixes=['_gold','_bronze'])
print(combine)
```

         NOC               Country  Total_gold  Total_bronze
    0    USA         United States      2088.0        1052.0
    1    URS          Soviet Union       838.0         584.0
    2    GBR        United Kingdom       498.0         505.0
    3    FRA                France       378.0         475.0
    4    GER               Germany       407.0         454.0
    ..   ...                   ...         ...           ...
    133  SEN               Senegal         NaN           NaN
    134  SUD                 Sudan         NaN           NaN
    135  TGA                 Tonga         NaN           NaN
    136  BDI               Burundi         1.0           NaN
    137  UAE  United Arab Emirates         1.0           NaN
    
    [138 rows x 4 columns]


### Merging on columns with non-matching labelsSpecifying columns to merge


```python
revenue = pd.read_csv('Sales/revenue.csv', delim_whitespace=True)
managers = pd.read_csv('Sales/managers.csv', delim_whitespace=True)
```


```python
revenue
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
      <th>city</th>
      <th>branch_id</th>
      <th>state</th>
      <th>revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Austin</td>
      <td>10</td>
      <td>TX</td>
      <td>100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Denver</td>
      <td>20</td>
      <td>CO</td>
      <td>83</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Springfield</td>
      <td>30</td>
      <td>IL</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mendocino</td>
      <td>47</td>
      <td>CA</td>
      <td>200</td>
    </tr>
  </tbody>
</table>
</div>




```python
managers
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
      <th>branch</th>
      <th>branch_id</th>
      <th>state</th>
      <th>manager</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Austin</td>
      <td>10</td>
      <td>TX</td>
      <td>Charlers</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Denver</td>
      <td>20</td>
      <td>CO</td>
      <td>Joel</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mendocino</td>
      <td>47</td>
      <td>CA</td>
      <td>Brett</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Springfield</td>
      <td>31</td>
      <td>MO</td>
      <td>Sally</td>
    </tr>
  </tbody>
</table>
</div>




```python
combine = pd.merge(revenue, managers, left_on='city', right_on='branch')
```


```python
combine
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
      <th>city</th>
      <th>branch_id_x</th>
      <th>state_x</th>
      <th>revenue</th>
      <th>branch</th>
      <th>branch_id_y</th>
      <th>state_y</th>
      <th>manager</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Austin</td>
      <td>10</td>
      <td>TX</td>
      <td>100</td>
      <td>Austin</td>
      <td>10</td>
      <td>TX</td>
      <td>Charlers</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Denver</td>
      <td>20</td>
      <td>CO</td>
      <td>83</td>
      <td>Denver</td>
      <td>20</td>
      <td>CO</td>
      <td>Joel</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Springfield</td>
      <td>30</td>
      <td>IL</td>
      <td>4</td>
      <td>Springfield</td>
      <td>31</td>
      <td>MO</td>
      <td>Sally</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mendocino</td>
      <td>47</td>
      <td>CA</td>
      <td>200</td>
      <td>Mendocino</td>
      <td>47</td>
      <td>CA</td>
      <td>Brett</td>
    </tr>
  </tbody>
</table>
</div>



### Merging with inner/outer join 
inner join is the default behavior.


```python
gold = gold.sort_values('Total',ascending=False).iloc[:5]
bronze = bronze.sort_values('Total',ascending=False).iloc[:5]
```


```python
combine = pd.merge(gold, bronze, on=['NOC','Country'], suffixes=['_gold','_bronze'], how='inner')
print(combine.head())
```

       NOC         Country  Total_gold  Total_bronze
    0  USA   United States      2088.0        1052.0
    1  URS    Soviet Union       838.0         584.0
    2  GBR  United Kingdom       498.0         505.0
    3  GER         Germany       407.0         454.0



```python
combine = pd.merge(gold, bronze, on=['NOC','Country'], suffixes=['_gold','_bronze'], how='outer')
print(combine.head())
```

       NOC         Country  Total_gold  Total_bronze
    0  USA   United States      2088.0        1052.0
    1  URS    Soviet Union       838.0         584.0
    2  GBR  United Kingdom       498.0         505.0
    3  ITA           Italy       460.0           NaN
    4  GER         Germany       407.0         454.0


### Merging with left/right join (Default)
Notice that Italy was picked up from `gold` but since it does not appear in `bronze`, it gets a Not a Number (NaN) value.


```python
combine = pd.merge(gold, bronze, on=['NOC','Country'], suffixes=['_gold','_bronze'], how='left')
print(combine.head())
```

       NOC         Country  Total_gold  Total_bronze
    0  USA   United States      2088.0        1052.0
    1  URS    Soviet Union       838.0         584.0
    2  GBR  United Kingdom       498.0         505.0
    3  ITA           Italy       460.0           NaN
    4  GER         Germany       407.0         454.0



```python
combine = pd.merge(gold, bronze, on=['NOC','Country'], suffixes=['_gold','_bronze'], how='right')
print(combine.head())
```

       NOC         Country  Total_gold  Total_bronze
    0  USA   United States      2088.0        1052.0
    1  URS    Soviet Union       838.0         584.0
    2  GBR  United Kingdom       498.0         505.0
    3  GER         Germany       407.0         454.0
    4  FRA          France         NaN         475.0


### Using .join()


```python
gold
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
      <th>NOC</th>
      <th>Country</th>
      <th>Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>USA</td>
      <td>United States</td>
      <td>2088.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>URS</td>
      <td>Soviet Union</td>
      <td>838.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GBR</td>
      <td>United Kingdom</td>
      <td>498.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>ITA</td>
      <td>Italy</td>
      <td>460.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GER</td>
      <td>Germany</td>
      <td>407.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
bronze
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
      <th>NOC</th>
      <th>Country</th>
      <th>Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>USA</td>
      <td>United States</td>
      <td>1052.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>URS</td>
      <td>Soviet Union</td>
      <td>584.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GBR</td>
      <td>United Kingdom</td>
      <td>505.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>FRA</td>
      <td>France</td>
      <td>475.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GER</td>
      <td>Germany</td>
      <td>454.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
gold.join(bronze, lsuffix='_gold', rsuffix='_bronze')
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
      <th>NOC_gold</th>
      <th>Country_gold</th>
      <th>Total_gold</th>
      <th>NOC_bronze</th>
      <th>Country_bronze</th>
      <th>Total_bronze</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>USA</td>
      <td>United States</td>
      <td>2088.0</td>
      <td>USA</td>
      <td>United States</td>
      <td>1052.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>URS</td>
      <td>Soviet Union</td>
      <td>838.0</td>
      <td>URS</td>
      <td>Soviet Union</td>
      <td>584.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GBR</td>
      <td>United Kingdom</td>
      <td>498.0</td>
      <td>GBR</td>
      <td>United Kingdom</td>
      <td>505.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>ITA</td>
      <td>Italy</td>
      <td>460.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GER</td>
      <td>Germany</td>
      <td>407.0</td>
      <td>GER</td>
      <td>Germany</td>
      <td>454.0</td>
    </tr>
  </tbody>
</table>
</div>



#### Left & right merging on multiple columns

In addition to the revenue and managers DataFrames from prior exercises, you have a DataFrame sales that summarizes units sold from specific branches (identified by city and state but not branch_id).

Once again, the managers DataFrame uses the label branch in place of city as in the other two DataFrames. Your task here is to employ left and right merges to preserve data and identify where data is missing.

By merging revenue and sales with a right merge, you can identify the missing revenue values. Here, you don't need to specify left_on or right_on because the columns to merge on have matching labels.

By merging sales and managers with a left merge, you can identify the missing manager. Here, the columns to merge on have conflicting labels, so you must specify left_on and right_on. In both cases, you're looking to figure out how to connect the fields in rows containing Springfield.


```python
import pandas as pd

revenue = pd.read_csv('Sales/revenue.csv', delim_whitespace=True)
managers = pd.read_csv('Sales/managers.csv', delim_whitespace=True)
sales = pd.read_csv('Sales/sales.csv', delim_whitespace=True)
```


```python
revenue.head()
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
      <th>city</th>
      <th>branch_id</th>
      <th>state</th>
      <th>revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Austin</td>
      <td>10</td>
      <td>TX</td>
      <td>100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Denver</td>
      <td>20</td>
      <td>CO</td>
      <td>83</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Springfield</td>
      <td>30</td>
      <td>IL</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mendocino</td>
      <td>47</td>
      <td>CA</td>
      <td>200</td>
    </tr>
  </tbody>
</table>
</div>




```python
managers.head()
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
      <th>branch</th>
      <th>branch_id</th>
      <th>state</th>
      <th>manager</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Austin</td>
      <td>10</td>
      <td>TX</td>
      <td>Charlers</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Denver</td>
      <td>20</td>
      <td>CO</td>
      <td>Joel</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mendocino</td>
      <td>47</td>
      <td>CA</td>
      <td>Brett</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Springfield</td>
      <td>31</td>
      <td>MO</td>
      <td>Sally</td>
    </tr>
  </tbody>
</table>
</div>




```python
sales.head()
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
      <th>city</th>
      <th>state</th>
      <th>units</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mendocino</td>
      <td>CA</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Denver</td>
      <td>CO</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Austin</td>
      <td>TX</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Springfield</td>
      <td>MO</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Springfield</td>
      <td>IL</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merge revenue and sales: revenue_and_sales
revenue_and_sales = pd.merge(revenue,sales, how='right', on=['city','state'])

# Print revenue_and_sales
print(revenue_and_sales)

# Merge sales and managers: sales_and_managers
sales_and_managers = pd.merge(sales, managers, how='left', left_on=['city','state'], right_on=['branch','state'])

# Print sales_and_managers
print(sales_and_managers)
```

              city  branch_id state  revenue  units
    0       Austin       10.0    TX    100.0      2
    1       Denver       20.0    CO     83.0      4
    2  Springfield       30.0    IL      4.0      1
    3    Mendocino       47.0    CA    200.0      1
    4  Springfield        NaN    MO      NaN      5
              city state  units       branch  branch_id   manager
    0    Mendocino    CA      1    Mendocino       47.0     Brett
    1       Denver    CO      4       Denver       20.0      Joel
    2       Austin    TX      2       Austin       10.0  Charlers
    3  Springfield    MO      5  Springfield       31.0     Sally
    4  Springfield    IL      1          NaN        NaN       NaN


### Special care needed with inner/outer join
Notice how the default merge drops the Springfield rows, while the default outer merge includes them twice.


```python
# Perform the first merge: merge_default
merge_default = pd.merge(sales_and_managers, revenue_and_sales)

# Print merge_default
print(merge_default)

# Perform the second merge: merge_outer
merge_outer = pd.merge(sales_and_managers, revenue_and_sales, how='outer')

# Print merge_outer
print(merge_outer)

# Perform the third merge: merge_outer_on
merge_outer_on = pd.merge(sales_and_managers, revenue_and_sales, how='outer', on=['city','state'])

# Print merge_outer_on
print(merge_outer_on)
```

            city state  units     branch  branch_id   manager  revenue
    0  Mendocino    CA      1  Mendocino       47.0     Brett    200.0
    1     Denver    CO      4     Denver       20.0      Joel     83.0
    2     Austin    TX      2     Austin       10.0  Charlers    100.0
              city state  units       branch  branch_id   manager  revenue
    0    Mendocino    CA      1    Mendocino       47.0     Brett    200.0
    1       Denver    CO      4       Denver       20.0      Joel     83.0
    2       Austin    TX      2       Austin       10.0  Charlers    100.0
    3  Springfield    MO      5  Springfield       31.0     Sally      NaN
    4  Springfield    IL      1          NaN        NaN       NaN      NaN
    5  Springfield    IL      1          NaN       30.0       NaN      4.0
    6  Springfield    MO      5          NaN        NaN       NaN      NaN
              city state  units_x       branch  branch_id_x   manager  \
    0    Mendocino    CA        1    Mendocino         47.0     Brett   
    1       Denver    CO        4       Denver         20.0      Joel   
    2       Austin    TX        2       Austin         10.0  Charlers   
    3  Springfield    MO        5  Springfield         31.0     Sally   
    4  Springfield    IL        1          NaN          NaN       NaN   
    
       branch_id_y  revenue  units_y  
    0         47.0    200.0        1  
    1         20.0     83.0        4  
    2         10.0    100.0        2  
    3          NaN      NaN        5  
    4         30.0      4.0        1  

