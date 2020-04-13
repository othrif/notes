---
title: "Looping Over Two Lists"
author: "Chris Albon"
date: 2017-12-20T11:53:49-07:00
description: "Looping over two lists using Python."
type: technical_note
draft: false
---

```python
# Create a list of length 3:
armies = ['Red Army', 'Blue Army', 'Green Army']

# Create a list of length 4:
units = ['Red Infantry', 'Blue Armor','Green Artillery','Orange Aircraft']
```


```python
# For each element in the first list,
for army, unit in zip(armies, units):
    # Display the corresponding index element of the second list:
    print(army, 'has the following options:', unit)
```

    Red Army has the following options: Red Infantry
    Blue Army has the following options: Blue Armor
    Green Army has the following options: Green Artillery


Notice that the fourth item of the second list, `orange aircraft`, did not display.
