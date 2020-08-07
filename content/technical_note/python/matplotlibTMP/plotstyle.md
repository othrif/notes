---
title: "Choosing a style"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
- Available styles: https://matplotlib.org/gallery/style_sheets/style_sheets_reference.html


```python
import matplotlib.pyplot as plt
import pandas as pd

seattle_weather = pd.read_csv('seattle_weather.csv').loc[:11]
austin_weather = pd.read_csv('austin_weather.csv')
seattle_weather['MONTH'] = pd.to_datetime(seattle_weather['DATE'], format='%m').dt.month_name().str.slice(stop=3)
austin_weather['MONTH'] = pd.to_datetime(austin_weather['DATE'], format='%m').dt.month_name().str.slice(stop=3)
```


```python
def plot_style(style='default'):
    plt.style.use(style)
    fig, ax = plt.subplots()

    # Add Seattle temperature data in each month with error bars
    ax.errorbar(seattle_weather['MONTH'], seattle_weather['MLY-TAVG-NORMAL'], yerr=seattle_weather['MLY-TAVG-STDDEV'])

    # Add Austin temperature data in each month with error bars
    ax.errorbar(austin_weather['MONTH'], austin_weather['MLY-TAVG-NORMAL'], yerr=austin_weather['MLY-TAVG-STDDEV']) 
    
    # Set the y-axis label
    ax.set_ylabel('Temperature (Fahrenheit)')

    plt.show()
```

### default


```python
plot_style('default')
```


![png](plotstyle_5_0.png)


### ggplot R style


```python
plot_style('ggplot')
```


![png](plotstyle_7_0.png)


### style: bmh


```python
plot_style('bmh')
```


![png](plotstyle_9_0.png)


### seaborn colorblind


```python
plot_style('seaborn-colorblind')
```


![png](plotstyle_11_0.png)


### tableau colorblind


```python
plot_style('tableau-colorblind10')
```


![png](plotstyle_13_0.png)


### black and white


```python
plot_style('grayscale')
```


![png](plotstyle_15_0.png)

