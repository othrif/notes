---
title: "Loop over maps, numpy arrays"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
###  Loop over maps


```python
# Definition of dictionary
europe = {'spain':'madrid', 'france':'paris', 'germany':'berlin',
          'norway':'oslo', 'italy':'rome', 'poland':'warsaw', 'austria':'vienna' }
          
# Iterate over europe
for k,v in europe.items():
    print('the capital of ' + str(k) +' is ' + str(v))
```

    the capital of spain is madrid
    the capital of france is paris
    the capital of germany is berlin
    the capital of norway is oslo
    the capital of italy is rome
    the capital of poland is warsaw
    the capital of austria is vienna


### Loop over 1D Numpy array


```python
import numpy as np
np_height = [1.2,32,23.2,23.1]
# For loop over np_height
for x in np_height:
    print(x)
```

    1.2
    32
    23.2
    23.1


### Loop over 2D Numpy array


```python
import numpy as np
baseball = [[180, 78.4],
            [215, 102.7],
            [210, 98.5],
            [188, 75.2]]
np_baseball = np.array(baseball)
```


```python
# flatten, printing rows sequentially
for x in np.nditer(np_baseball):
    print(x)
```

    180.0
    78.4
    215.0
    102.7
    210.0
    98.5
    188.0
    75.2

