---
title: "Music recommender system with full pipeline"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
import pandas as pd
from scipy.sparse import csr_matrix
df = pd.read_csv('artists/scrobbler-small-sample.csv', index_col=0)
artists = csr_matrix(df.transpose())
artist_names = [x.strip('\n').split(' ')[0] for x in open('artists/artists.csv').readlines()]
```

computed the normalized NMF features:


```python
# Perform the necessary imports
from sklearn.decomposition import NMF
from sklearn.preprocessing import Normalizer, MaxAbsScaler
from sklearn.pipeline import make_pipeline

# Create a MaxAbsScaler: scaler
scaler = MaxAbsScaler()

# Create an NMF model: nmf
nmf = NMF(n_components=20)

# Create a Normalizer: normalizer
normalizer = Normalizer()

# Create a pipeline: pipeline
pipeline = make_pipeline(scaler, nmf, normalizer)

# Apply fit_transform to artists: norm_features
norm_features = pipeline.fit_transform(artists)
norm_features
```




    array([[0.00000000e+00, 0.00000000e+00, 4.34316939e-01, 2.88405912e-01,
            3.35804758e-01, 0.00000000e+00, 9.58344722e-02, 4.31840755e-01,
            2.20635850e-01, 1.32500967e-01, 2.21954101e-01, 0.00000000e+00,
            0.00000000e+00, 1.91923347e-01, 3.10995073e-01, 8.17897722e-02,
            3.94469409e-02, 2.29707948e-01, 2.94175098e-01, 1.52158259e-01],
           [8.96329209e-01, 3.05802585e-01, 5.40945254e-02, 4.56602807e-02,
            8.00709336e-02, 1.50733837e-01, 6.70677029e-03, 2.80649683e-04,
            3.77263930e-02, 4.57270986e-02, 3.64936967e-02, 1.18623583e-01,
            1.46168774e-01, 1.33650249e-01, 3.53962415e-02, 2.21133351e-02,
            7.07914479e-02, 1.96741509e-02, 0.00000000e+00, 6.00404816e-02]])




```python
# Import pandas
import pandas as pd

# Create a DataFrame: df
df = pd.DataFrame(norm_features, index=artist_names)
display(df)
# Select row of 'Bruce Springsteen': artist
artist = df.loc['Bruce Springsteen']

# Compute cosine similarities: similarities
similarities = df.dot(artist)

# Display those with highest cosine similarity
print(similarities.nlargest())
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    ~/Library/Python/3.7/lib/python/site-packages/pandas/core/internals/managers.py in create_block_manager_from_blocks(blocks, axes)
       1656 
    -> 1657         mgr = BlockManager(blocks, axes)
       1658         mgr._consolidate_inplace()


    ~/Library/Python/3.7/lib/python/site-packages/pandas/core/internals/managers.py in __init__(self, blocks, axes, do_integrity_check)
        138         if do_integrity_check:
    --> 139             self._verify_integrity()
        140 


    ~/Library/Python/3.7/lib/python/site-packages/pandas/core/internals/managers.py in _verify_integrity(self)
        333             if block._verify_integrity and block.shape[1:] != mgr_shape[1:]:
    --> 334                 construction_error(tot_items, block.shape[1:], self.axes)
        335         if len(self.items) != tot_items:


    ~/Library/Python/3.7/lib/python/site-packages/pandas/core/internals/managers.py in construction_error(tot_items, block_shape, axes, e)
       1693         raise ValueError("Empty data passed with indices specified.")
    -> 1694     raise ValueError(f"Shape of passed values is {passed}, indices imply {implied}")
       1695 


    ValueError: Shape of passed values is (2, 20), indices imply (111, 20)

    
    During handling of the above exception, another exception occurred:


    ValueError                                Traceback (most recent call last)

    <ipython-input-218-62a834bc3aab> in <module>
          3 
          4 # Create a DataFrame: df
    ----> 5 df = pd.DataFrame(norm_features, index=artist_names)
          6 display(df)


    ~/Library/Python/3.7/lib/python/site-packages/pandas/core/frame.py in __init__(self, data, index, columns, dtype, copy)
        462                 mgr = init_dict({data.name: data}, index, columns, dtype=dtype)
        463             else:
    --> 464                 mgr = init_ndarray(data, index, columns, dtype=dtype, copy=copy)
        465 
        466         # For data is list-like, or Iterable (will consume into list)


    ~/Library/Python/3.7/lib/python/site-packages/pandas/core/internals/construction.py in init_ndarray(values, index, columns, dtype, copy)
        208         block_values = [values]
        209 
    --> 210     return create_block_manager_from_blocks(block_values, [columns, index])
        211 
        212 


    ~/Library/Python/3.7/lib/python/site-packages/pandas/core/internals/managers.py in create_block_manager_from_blocks(blocks, axes)
       1662         blocks = [getattr(b, "values", b) for b in blocks]
       1663         tot_items = sum(b.shape[0] for b in blocks)
    -> 1664         construction_error(tot_items, blocks[0].shape[1:], axes, e)
       1665 
       1666 


    ~/Library/Python/3.7/lib/python/site-packages/pandas/core/internals/managers.py in construction_error(tot_items, block_shape, axes, e)
       1692     if block_shape[0] == 0:
       1693         raise ValueError("Empty data passed with indices specified.")
    -> 1694     raise ValueError(f"Shape of passed values is {passed}, indices imply {implied}")
       1695 
       1696 


    ValueError: Shape of passed values is (2, 20), indices imply (111, 20)



```python

```
