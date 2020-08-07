---
title: "Customize plots with ax and fig"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
- Matplotlib markers: https://matplotlib.org/api/markers_api.html
- Matplotlib linestyles: https://matplotlib.org/3.1.0/gallery/lines_bars_and_markers/linestyles.html


```python
import matplotlib.pyplot as plt
import pandas as pd

seattle_weather = pd.read_csv('seattle_weather.csv').loc[:11]
austin_weather = pd.read_csv('austin_weather.csv')
seattle_weather['MONTH'] = pd.to_datetime(seattle_weather['DATE'], format='%m').dt.month_name().str.slice(stop=3)
austin_weather['MONTH'] = pd.to_datetime(austin_weather['DATE'], format='%m').dt.month_name().str.slice(stop=3)
```


```python

# Create a figure and an array of axes: 2 rows, 1 column with shared y axis
fig, ax = plt.subplots(2, 1, sharey=True)

# Plot Seattle precipitation data in the top axes
ax[0].plot(seattle_weather['MONTH'], seattle_weather['MLY-PRCP-NORMAL'], marker = 'o', color = 'b')
ax[0].plot(seattle_weather['MONTH'], seattle_weather['MLY-PRCP-25PCTL'], marker = None, color = 'b', linestyle = '--')
ax[0].plot(seattle_weather['MONTH'], seattle_weather['MLY-PRCP-75PCTL'], marker = None, color = 'b', linestyle = '--')

# Plot Austin precipitation data in the bottom axes
ax[1].plot(austin_weather['MONTH'], austin_weather['MLY-PRCP-NORMAL'], marker = 'v', color = 'r')
ax[1].plot(austin_weather['MONTH'], austin_weather['MLY-PRCP-25PCTL'], marker = None, color = 'r', linestyle = '--')
ax[1].plot(austin_weather['MONTH'], austin_weather['MLY-PRCP-75PCTL'], marker = None, color = 'r', linestyle = '--')

ax[0].set_title('Weather patterns in Austin and Seattle')
ax[0].set_ylabel('Precipitation (inches)')
ax[1].set_ylabel('Precipitation (inches)')
ax[1].set_xlabel('Time (months)')

plt.show()
```


![png](ax_fig_files/ax_fig_3_0.png)

