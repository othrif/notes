---
title: "Split text column into multiple new columns"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
See: https://github.com/dennisbakhuis/Tutorials/blob/master/B_Pandas_tips/2-%20Split%20text%20column%20into%20multiple%20new%20columns.ipynb


```python
import pandas as pd

df = pd.DataFrame([
    {'path': 'train/data_shard_1.csv'},
    {'path': 'train/data_shard_2.csv'},
    {'path': 'train/data_shard_3.csv'},
    {'path': 'test/data_shard_1.csv'},
    {'path': 'test/data_shard_2.csv'},
])

df = (df
    .join(df
        .loc[:, 'path']
        .str.split('/', expand=True)
        .rename(columns={0: 'folder', 1: 'filename'})
    )
)

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>path</th>
      <th>folder</th>
      <th>filename</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>train/data_shard_1.csv</td>
      <td>train</td>
      <td>data_shard_1.csv</td>
    </tr>
    <tr>
      <th>1</th>
      <td>train/data_shard_2.csv</td>
      <td>train</td>
      <td>data_shard_2.csv</td>
    </tr>
    <tr>
      <th>2</th>
      <td>train/data_shard_3.csv</td>
      <td>train</td>
      <td>data_shard_3.csv</td>
    </tr>
    <tr>
      <th>3</th>
      <td>test/data_shard_1.csv</td>
      <td>test</td>
      <td>data_shard_1.csv</td>
    </tr>
    <tr>
      <th>4</th>
      <td>test/data_shard_2.csv</td>
      <td>test</td>
      <td>data_shard_2.csv</td>
    </tr>
  </tbody>
</table>
</div>


