---
title: "Function as an object, nested functions"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Nested functions
Notice how we assign the return value from `create_math_function()` to the `add` and `subtract` variables in the script. Since `create_math_function()` returns a function, we can then call those variables as functions.


```python
def create_math_function(func_name):
  if func_name == 'add':
    def add(a, b):
      return a + b
    return add
  elif func_name == 'subtract':
    # Define the subtract() function
    def subtract(a,b):
        return a - b
    return subtract
  else:
    print("I don't know that one")
    
add = create_math_function('add')
print('5 + 2 = {}'.format(add(5, 2)))

subtract = create_math_function('subtract')
print('5 - 2 = {}'.format(subtract(5, 2)))
```

    5 + 2 = 7
    5 - 2 = 3

