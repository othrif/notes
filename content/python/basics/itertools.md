---
title: "Itertools:groupby()"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### `groupby()`

Function call: `functools.groupby(iterable[, key])`   

Make an iterator that returns consecutive keys and groups from the iterable. Similar to the `uniq` filter in Unix.

### Count number of occurences


```python
import itertools
for key, group in itertools.groupby('1122111100'):
    print(key, 'count:', len(list(group)))
```

    1 count: 2
    2 count: 2
    1 count: 4
    0 count: 2


### Use a cutom key function


```python
import itertools
l = [("a", 1), ("a", 2), ("b", 3), ("b", 4)]
key_f = lambda x: x[0]

for key, group in itertools.groupby(l, key_f):
    print(key + ": " + str(list(group)))

```

    a: [('a', 1), ('a', 2)]
    b: [('b', 3), ('b', 4)]


### Implement a group by in python using dict()


```python
data = [ ("integer", 1), ("string", "a"), ("float", 1.0), ("integer", 2)]
groups = {}
for group, value in data:
    # Add new group-value pair to `groups`
    if group not in groups:
        groups.update({group: [value]})
    # Add `value` to existing group's value list
    else:
        groups[group].append(value)


print(groups)
```

    {'integer': [1, 2], 'string': ['a'], 'float': [1.0]}

