---
title: "Functions"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Exit from function with conditions


```python
outer_condition=True
condition_a=True
condition_b=False


def some_function():
    if condition_a:
        # do something and return early
        print(f'condition a satisfied!')
        return
    if condition_b:
        # do something else and return early
        print(f'condition b satisfied!')
        return
    return

if outer_condition:
    some_function()
```

    condition a satisfied!


### Passing a list as an argument


```python
def my_function(food):
  for x in food:
    print(x)

fruits = ["apple", "banana", "cherry"]

my_function(fruits)
```

    apple
    banana
    cherry



```python

```
