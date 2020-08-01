---
title: "Perform a t-test"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import pandas as pd
laptops = pd.read_csv('laptops.csv' , encoding='latin-1', index_col=0) # added encoding because of errors
laptops = laptops.loc[laptops['Company'].isin(['Asus', 'Toshiba'])]
laptops = laptops[['Company','Price_euros']]
laptops.columns = ['Company', 'Price']
```


```python
# Display the mean price for each group
prices = laptops.groupby('Company').mean()
print(prices)
```

                   Price
    Company             
    Asus     1104.169367
    Toshiba  1267.812500



```python
# Assign the prices of each group
asus = laptops[laptops['Company'] == 'Asus']['Price']
toshiba = laptops[laptops['Company'] == 'Toshiba']['Price']

# Run the t-test
from scipy.stats import ttest_ind
tstat, pval = ttest_ind(asus, toshiba)
print('{0:0.3f}'.format(pval))
```

    0.133


With a p-value of .133, we cannot reject the null hypothesis! There's not enough evidence here to conclude that Toshiba laptops are significantly more expensive than Asus. With that being said, .133 is fairly close to reasonable significance so we may want to run another test or examine this further.
