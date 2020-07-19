---
title: "Arithmetic with Series & DataFrames"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Broadcasting in arithmetic formulas
In only three lines of code, you converted the units of 365 data points (over three columns) from degrees Fahrenheit to degrees Celsius.


```python
import pandas as pd
weather = pd.read_csv('pittsburgh2013.csv')
```


```python
weather.shape
```




    (365, 23)




```python
# Extract selected columns from weather as new DataFrame: temps_f
temps_f = weather.loc[:,['Min TemperatureF','Mean TemperatureF', 'Max TemperatureF']]

# Convert temps_f to celsius: temps_c
temps_c = (temps_f-32) * 5/9

# Rename 'F' in column names with 'C': temps_c.columns
temps_c.columns = temps_c.columns.str.replace('F','C')

# Print first 5 rows of temps_c
print(temps_c.head())
```

       Min TemperatureC  Mean TemperatureC  Max TemperatureC
    0         -6.111111          -2.222222          0.000000
    1         -8.333333          -6.111111         -3.888889
    2         -8.888889          -4.444444          0.000000
    3         -2.777778          -2.222222         -1.111111
    4         -3.888889          -1.111111          1.111111


### Computing percentage growth of GDP


```python
import pandas as pd

# Read 'GDP.csv' into a DataFrame: gdp
gdp = pd.read_csv('GDP/gdp_usa.csv', index_col='DATE', parse_dates=True)

# Slice all the gdp data from 2008 onward: post2008
post2008 = gdp.loc['2008-01-01':,:]

# Print the last 8 rows of post2008
print(post2008.tail(8))
print(post2008.head(8))

# Resample post2008 by year, keeping last(): yearly
# using the alias 'A' for annual frequency
# use the aggregation method .last() to select the last element when resampling.
yearly = post2008.resample('A').last() 

# Print yearly
print(yearly)

# Compute percentage growth of yearly: yearly['growth']
yearly['growth'] = yearly.pct_change()*100

# Print yearly again
print(yearly)
```

                  VALUE
    DATE               
    2014-07-01  17569.4
    2014-10-01  17692.2
    2015-01-01  17783.6
    2015-04-01  17998.3
    2015-07-01  18141.9
    2015-10-01  18222.8
    2016-01-01  18281.6
    2016-04-01  18436.5
                  VALUE
    DATE               
    2008-01-01  14668.4
    2008-04-01  14813.0
    2008-07-01  14843.0
    2008-10-01  14549.9
    2009-01-01  14383.9
    2009-04-01  14340.4
    2009-07-01  14384.1
    2009-10-01  14566.5
                  VALUE
    DATE               
    2008-12-31  14549.9
    2009-12-31  14566.5
    2010-12-31  15230.2
    2011-12-31  15785.3
    2012-12-31  16297.3
    2013-12-31  16999.9
    2014-12-31  17692.2
    2015-12-31  18222.8
    2016-12-31  18436.5
                  VALUE    growth
    DATE                         
    2008-12-31  14549.9       NaN
    2009-12-31  14566.5  0.114090
    2010-12-31  15230.2  4.556345
    2011-12-31  15785.3  3.644732
    2012-12-31  16297.3  3.243524
    2013-12-31  16999.9  4.311144
    2014-12-31  17692.2  4.072377
    2015-12-31  18222.8  2.999062
    2016-12-31  18436.5  1.172707


### Converting currency of stocks
Stock prices in US Dollars for the S&P 500 in 2015 have been obtained from Yahoo Finance. The files `sp500.csv` for sp500 and `exchange.csv` for the exchange rates are both provided.

Using the daily exchange rate to Pounds Sterling, your task is to convert both the Open and Close column prices.


```python
# Import pandas
import pandas as pd

# Read 'sp500.csv' into a DataFrame: sp500
sp500 = pd.read_csv('sp500.csv', parse_dates=True, index_col='Date')

# Read 'exchange.csv' into a DataFrame: exchange
exchange = pd.read_csv('exchange.csv', parse_dates=True, index_col='Date')

# Subset 'Open' & 'Close' columns from sp500: dollars
dollars = sp500.loc[:,['Open','Close']]

# Print the head of dollars
print(dollars.head())

# Convert dollars to pounds: pounds
pounds = dollars.multiply(exchange['GBP/USD'], axis='rows')

# Print the head of pounds
print(pounds.head())
```

                       Open        Close
    Date                                
    2015-01-02  2058.899902  2058.199951
    2015-01-05  2054.439941  2020.579956
    2015-01-06  2022.150024  2002.609985
    2015-01-07  2005.550049  2025.900024
    2015-01-08  2030.609985  2062.139893
                       Open        Close
    Date                                
    2015-01-02  1340.364425  1339.908750
    2015-01-05  1348.616555  1326.389506
    2015-01-06  1332.515980  1319.639876
    2015-01-07  1330.562125  1344.063112
    2015-01-08  1343.268811  1364.126161

