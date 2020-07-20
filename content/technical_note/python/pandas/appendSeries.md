---
title: "Appending pandas Series"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Basics
Load sales data from the months January, February, and March into DataFrames. Then, extract Series with the 'Units' column from each and append them together with method chaining using .append().

To check that the stacking worked, you'll print slices from these Series, and finally, you'll add the result to figure out the total units sold in the first quarter.


```python
# Import pandas
import pandas as pd

# Load 'sales-jan-2015.csv' into a DataFrame: jan
jan = pd.read_csv('Sales/sales-jan-2015.csv', parse_dates=True,index_col='Date')

# Load 'sales-feb-2015.csv' into a DataFrame: feb
feb = pd.read_csv('Sales/sales-feb-2015.csv', parse_dates=True,index_col='Date')

# Load 'sales-mar-2015.csv' into a DataFrame: mar
mar = pd.read_csv('Sales/sales-mar-2015.csv', parse_dates=True,index_col='Date')

# Extract the 'Units' column from jan: jan_units
jan_units = jan['Units']

# Extract the 'Units' column from feb: feb_units
feb_units = feb['Units']

# Extract the 'Units' column from mar: mar_units
mar_units = mar['Units']

# Append feb_units and then mar_units to jan_units: quarter1
quarter1 = jan_units.append(feb_units).append(mar_units)

# Print the first slice from quarter1
print(quarter1.loc['jan 27, 2015':'feb 2, 2015'])

# Print the second slice from quarter1
print(quarter1.loc['feb 26, 2015':'mar 7, 2015'])

# Compute & print total sales in quarter1
print(quarter1.sum())
```

    Date
    2015-01-27 07:11:55    18
    2015-02-02 08:33:01     3
    2015-02-02 20:54:49     9
    Name: Units, dtype: int64
    Date
    2015-02-26 08:57:45     4
    2015-02-26 08:58:51     1
    2015-03-06 10:11:45    17
    2015-03-06 02:03:56    17
    Name: Units, dtype: int64
    642


### Concatenating pandas Series along row axis
achieve the same result as above by concatenating Series instead


```python
# Initialize empty list: units
units = []

# Build the list of Series
for month in [jan, feb, mar]:
    units.append(month['Units'])

# Concatenate the list: quarter1
quarter1 = pd.concat(units, axis='rows')

# Print slices from quarter1
print(quarter1.loc['jan 27, 2015':'feb 2, 2015'])
print(quarter1.loc['feb 26, 2015':'mar 7, 2015'])
```

    Date
    2015-01-27 07:11:55    18
    2015-02-02 08:33:01     3
    2015-02-02 20:54:49     9
    Name: Units, dtype: int64
    Date
    2015-02-26 08:57:45     4
    2015-02-26 08:58:51     1
    2015-03-06 10:11:45    17
    2015-03-06 02:03:56    17
    Name: Units, dtype: int64


### 



```python

```
