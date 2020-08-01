---
title: "Perform a z-test"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
from statsmodels.stats.proportion import proportions_ztest
count = 5
nobs = 83
value = .05
stat, pval = proportions_ztest(count, nobs, value)
print(f'p-value={pval:0.3f}, sig={stat:0.3f} sigma')
```

    p-value=0.695, sig=0.392 sigma



```python
import numpy as np
from statsmodels.stats.proportion import proportions_ztest
count = np.array([5, 12])
nobs = np.array([83, 99])
stat, pval = proportions_ztest(count, nobs)
print(f'p-value={pval:0.3f}, sig={stat:0.3f} sigma')
```

    p-value=0.159, sig=-1.408 sigma


### Example


```python
import pandas as pd
results = pd.read_csv('ab_data.csv' , encoding='latin-1', index_col=0) # added encoding because of errors
results = results[['group','converted']]
results.columns = ['Group','Converted']
# Assign and print the conversion rate for each group
conv_rates = results.groupby('Group').mean()
print(conv_rates)
```

               Converted
    Group               
    control     0.120399
    treatment   0.118920



```python
# Assign the number of conversions and total trials
num_control = results[results['Group'] == 'control']['Converted'].sum()
total_control = len(results[results['Group'] == 'control'])

# Assign the number of conversions and total trials
num_treat = results[results['Group'] == 'treatment']['Converted'].sum()
total_treat = len(results[results['Group'] == 'treatment'])

import numpy as np
from statsmodels.stats.proportion import proportions_ztest
count = np.array([num_treat, num_control]) 
nobs = np.array([total_treat, total_control])

# Run the z-test and print the result 
stat, pval = proportions_ztest(count, nobs, alternative="larger")
print(f'p-value={pval:0.3f}, sig={stat:0.3f} sigma')
```

    p-value=0.892, sig=-1.237 sigma


p-value > 0.05, cannot reject the null hypothesis
