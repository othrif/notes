---
title: "Creating DataFrames"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
- From a list of dictionaries: construct row by row
- From a dictionary of lists: construct column by column

### From a list of dictionaries


```python
import pandas as pd 

# Create a list of dictionaries with new data
avocados_list = [
    {'date': '2019-11-03', 'small_sold': 10376832, 'large_sold': 7835071},
    {'date': '2019-11-10', 'small_sold': 10717154, 'large_sold': 8561348}
]

# Convert list into DataFrame
avocados_2019 = pd.DataFrame(avocados_list)

# Print the new DataFrame
print(avocados_2019)
```

             date  small_sold  large_sold
    0  2019-11-03    10376832     7835071
    1  2019-11-10    10717154     8561348


### From a dictionary of lists


```python
# Create a dictionary of lists with new data
avocados_dict = {
    'date': ['2019-11-17', '2019-12-01'],
    'small_sold': [10859987, 9291631],
    'large_sold': [7674135, 6238096]
}

# Convert dictionary into DataFrame
avocados_2019 = pd.DataFrame(avocados_dict)

# Print the new DataFrame
print(avocados_2019)
```

             date  small_sold  large_sold
    0  2019-11-17    10859987     7674135
    1  2019-12-01     9291631     6238096

