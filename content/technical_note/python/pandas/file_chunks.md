---
title: "Load data in chunks"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Loading data in chunks
the data we have to process reaches a size that is too much for a computer's memory to handle. A solution to this is to process an entire data source chunk by chunk, instead of a single go all at once.


```python
import pandas as pd
def count_entries(csv_file, c_size, colname):
    """Return a dictionary with counts of
    occurrences as value for each key."""
    
    # Initialize an empty dictionary: counts_dict
    counts_dict = {}

    # Iterate over the file chunk by chunk
    for chunk in pd.read_csv(csv_file, chunksize=c_size):

        # Iterate over the column in DataFrame
        for entry in chunk[colname]:
            if entry in counts_dict.keys():
                counts_dict[entry] += 1
            else:
                counts_dict[entry] = 1

    # Return counts_dict
    return counts_dict
```


```python
result_counts = count_entries(csv_file='../datasets/tweets.csv',c_size=10, colname='lang')
print(result_counts)
```

    {'en': 97, 'et': 1, 'und': 2}

