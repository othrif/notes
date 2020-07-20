---
title: "Outer and inner joins"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Joins
Joining tables: Combining rows of multiple tables

#### Outer join
* Missing fields filled with NaN
* Union of index sets (all labels, no repetition)

#### Inner join
* Intersection of index sets (only common labels)



```python
import pandas as pd

bronze = pd.read_csv('SummerOlypmic/bronze_top5.csv')
silver = pd.read_csv('SummerOlypmic/silver_top5.csv')
gold = pd.read_csv('SummerOlypmic/gold_top5.csv')
```

### Inner join


```python
# Create the list of DataFrames: medal_list
medal_list = [bronze, silver, gold]

# Concatenate medal_list horizontally using an inner join: medals
medals = pd.concat(medal_list, axis=1, keys=['bronze','silver', 'gold'], join='inner')

# Print medals
print(medals)
```

               bronze                  silver                    gold        
              Country   Total         Country   Total         Country   Total
    0   United States  1052.0   United States  1195.0   United States  2088.0
    1    Soviet Union   584.0    Soviet Union   627.0    Soviet Union   838.0
    2  United Kingdom   505.0  United Kingdom   591.0  United Kingdom   498.0
    3          France   475.0          France   461.0           Italy   460.0
    4         Germany   454.0           Italy   394.0         Germany   407.0


### Outer join


```python
# Create the list of DataFrames: medal_list
medal_list = [bronze, silver, gold]

# Concatenate medal_list horizontally using an inner join: medals
medals = pd.concat(medal_list, axis=1, keys=['bronze','silver', 'gold'], join='outer')

# Print medals
print(medals)
```

               bronze                  silver                    gold        
              Country   Total         Country   Total         Country   Total
    0   United States  1052.0   United States  1195.0   United States  2088.0
    1    Soviet Union   584.0    Soviet Union   627.0    Soviet Union   838.0
    2  United Kingdom   505.0  United Kingdom   591.0  United Kingdom   498.0
    3          France   475.0          France   461.0           Italy   460.0
    4         Germany   454.0           Italy   394.0         Germany   407.0


### More advanced resampling & concatenating


```python
china = pd.read_csv('GDP/gdp_china.csv', parse_dates=True, index_col=0, )
us = pd.read_csv('GDP/gdp_usa.csv', parse_dates=True, index_col=0)
print(china.head()) # need to change GDP > China 
print(us.head()) # need to change VALUE > US
```

                      GDP
    Year                 
    1960-01-01  59.184116
    1961-01-01  49.557050
    1962-01-01  46.685179
    1963-01-01  50.097303
    1964-01-01  59.062255
                VALUE
    DATE             
    1947-01-01  243.1
    1947-04-01  246.3
    1947-07-01  250.1
    1947-10-01  260.3
    1948-01-01  266.2



```python
# Resample and tidy china: china_annual
china_annual = china.resample('A').last().pct_change(10).dropna()

# Resample and tidy us: us_annual
us_annual = us.resample('A').last().pct_change(10).dropna()

# Concatenate china_annual and us_annual: gdp
gdp = pd.concat([china_annual, us_annual], join='inner', axis=1)

# Resample gdp and print
print(gdp.resample('10A').last())
```

                     GDP     VALUE
    Year                          
    1970-12-31  0.546128  1.017187
    1980-12-31  1.072537  1.742556
    1990-12-31  0.892820  1.012126
    2000-12-31  2.357522  0.738632
    2010-12-31  4.011081  0.454332
    2020-12-31  3.789936  0.361780

