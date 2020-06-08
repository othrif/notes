---
title: "Loops with DataFrames"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
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
cars2 = cars
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


### Loop over DataFrame
Iterating over a Pandas DataFrame is typically done with the `iterrows()`     
On every run, a Pandas Series is generated.


```python
for lab, row in cars.iterrows() :
    print(lab)
    print(row)
```

    US
    country         United States
    drives_right             True
    cars_per_cap              809
    Name: US, dtype: object
    AUS
    country         Australia
    drives_right        False
    cars_per_cap          731
    Name: AUS, dtype: object
    JPN
    country         Japan
    drives_right    False
    cars_per_cap      588
    Name: JPN, dtype: object
    IN
    country         India
    drives_right    False
    cars_per_cap       18
    Name: IN, dtype: object
    RU
    country         Russia
    drives_right      True
    cars_per_cap       200
    Name: RU, dtype: object
    MOR
    country         Morocco
    drives_right       True
    cars_per_cap         70
    Name: MOR, dtype: object
    EG
    country         Egypt
    drives_right     True
    cars_per_cap       45
    Name: EG, dtype: object



```python
# Pick a specific element in the series
for lab, row in cars.iterrows() :
    print(lab+':'+str(row['cars_per_cap']))
```

    US:809
    AUS:731
    JPN:588
    IN:18
    RU:200
    MOR:70
    EG:45


### Add a new column with for-loop
Adding a new column with for-loop is not very efficient. On every iteration, you're creating a new Pandas Series.


```python
for lab,row in cars.iterrows():
    cars.loc[lab,'COUNTRY'] = row['country'].upper()
print(cars)
```

               country  drives_right  cars_per_cap        COUNTRY
    US   United States          True           809  UNITED STATES
    AUS      Australia         False           731      AUSTRALIA
    JPN          Japan         False           588          JAPAN
    IN           India         False            18          INDIA
    RU          Russia          True           200         RUSSIA
    MOR        Morocco          True            70        MOROCCO
    EG           Egypt          True            45          EGYPT



```python
cars2['COUNTRY'] = cars['country'].apply(str.upper)
print(cars)
```

               country  drives_right  cars_per_cap        COUNTRY
    US   United States          True           809  UNITED STATES
    AUS      Australia         False           731      AUSTRALIA
    JPN          Japan         False           588          JAPAN
    IN           India         False            18          INDIA
    RU          Russia          True           200         RUSSIA
    MOR        Morocco          True            70        MOROCCO
    EG           Egypt          True            45          EGYPT



```python
cars2['Length'] = cars['country'].apply(len)
print(cars)
```

               country  drives_right  cars_per_cap        COUNTRY  Length
    US   United States          True           809  UNITED STATES      13
    AUS      Australia         False           731      AUSTRALIA       9
    JPN          Japan         False           588          JAPAN       5
    IN           India         False            18          INDIA       5
    RU          Russia          True           200         RUSSIA       6
    MOR        Morocco          True            70        MOROCCO       7
    EG           Egypt          True            45          EGYPT       5

