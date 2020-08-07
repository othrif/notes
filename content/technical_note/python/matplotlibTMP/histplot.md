---
title: "Make comnparison histograms"
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
```


```python
fig, ax = plt.subplots()

# Plot a histogram of "Weight" for mens_rowing
ax.hist(mens_rowing['Weight'], label='Rowing', histtype='step', bins=5)

# Compare to histogram of "Weight" for mens_gymnastics
ax.hist(mens_gymnastics['Weight'], label='Gymnastics', histtype='step', bins=5)

ax.set_xlabel("Weight (kg)")
ax.set_ylabel("# of observations")

# Add the legend and show the Figure
ax.legend()
plt.show()

```


![png](histplot_2_0.png)

