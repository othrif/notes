---
title: "Show errors in bar, plot, and boxplot"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import matplotlib.pyplot as plt
import pandas as pd

summer2016 = pd.read_csv('summer2016.csv', index_col=0)
mens_rowing = summer2016[summer2016['Sport'] == 'Rowing']
mens_gymnastics = summer2016[summer2016['Sport'] == 'Gymnastics']


seattle_weather = pd.read_csv('seattle_weather.csv').loc[:11]
austin_weather = pd.read_csv('austin_weather.csv')
seattle_weather['MONTH'] = pd.to_datetime(seattle_weather['DATE'], format='%m').dt.month_name().str.slice(stop=3)
austin_weather['MONTH'] = pd.to_datetime(austin_weather['DATE'], format='%m').dt.month_name().str.slice(stop=3)
```

### Adding error-bars to a bar chart


```python
fig, ax = plt.subplots()

# Add a bar for the rowing "Height" column mean/std
ax.bar("Rowing", mens_rowing['Height'].mean(), yerr=mens_rowing['Height'].std())

# Add a bar for the gymnastics "Height" column mean/std
ax.bar("Gymnastics", mens_gymnastics['Height'].mean(), yerr=mens_gymnastics['Height'].std())


# Label the y-axis
ax.set_ylabel("Height (cm)")

plt.show()
```


![png](errorsplot_3_0.png)


### Adding error-bars to a plot


```python
fig, ax = plt.subplots()

# Add Seattle temperature data in each month with error bars
ax.errorbar(seattle_weather['MONTH'], seattle_weather['MLY-TAVG-NORMAL'], yerr=seattle_weather['MLY-TAVG-STDDEV'])

# Add Austin temperature data in each month with error bars
ax.errorbar(austin_weather['MONTH'], austin_weather['MLY-TAVG-NORMAL'], yerr=austin_weather['MLY-TAVG-STDDEV']) 

# Set the y-axis label
ax.set_ylabel('Temperature (Fahrenheit)')

plt.show()
```


![png](errorsplot_5_0.png)


### Creating boxplots
Tell us what the median of the distribution is, what the inter-quartile range is and also what the expected range of approximately 99% of the data should be. Outliers beyond this range are particularly highlighted.


```python
fig, ax = plt.subplots()

# Add a boxplot for the "Height" column in the DataFrames
ax.boxplot([mens_rowing['Height'], mens_gymnastics['Height']])

# Add x-axis tick labels:
ax.set_xticklabels(['Rowing', 'Gymnastics'])

# Add a y-axis label
ax.set_ylabel('Height (cm)')

plt.show()
```


![png](errorsplot_7_0.png)



```python
fig, ax = plt.subplots()
ax.hist(mens_rowing['Height'], histtype='step', label='Rowing')
ax.hist(mens_gymnastics['Height'], histtype='step', label='Gymnastics')
ax.legend()
plt.show()
```


![png](errorsplot_8_0.png)

