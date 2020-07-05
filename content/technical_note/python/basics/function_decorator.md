---
title: "Defining a decorator @decorator"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Defining a decorator
The decorator is a function that takes another function as an argument and modifies its behavior. Add `@` before the decorator function name without `()`. 
The syntax 
``` python 
@decorator
def function():
    pass
```
is equivalent to
``` python 
def function():
    pass

function = decorator(function)
```


```python
def parent(func):
    # nested function
    def child(a,b):
        return func(a*2,b*2)
    return child

def multiply(a,b):
    return a*b

multiply = parent(multiply)
multiply(1,2)
```




    8




```python
def parent(func):
    # nested function
    def child(a,b):
        return func(a*2,b*2)
    return child

@parent
def multiply(a,b):
    return a*b

multiply(1,2)
```




    8



### Verifying decorator
The decorator `print_before_and_after()` defines a nested function `wrapper()` that calls whatever function gets passed to `print_before_and_after()`. `wrapper()` adds a little something else to the function call by printing one message before the decorated function is called and another right afterwards. Since `print_before_and_after()` returns the new `wrapper()` function, we can use it as a decorator to decorate the `multiply()` function.


```python
def print_before_and_after(func):
  def wrapper(*args):
    print('Before {}'.format(func.__name__))
    # Call the function being decorated with *args
    func(*args)
    print('After {}'.format(func.__name__))
  # Return the nested function
  return wrapper

@print_before_and_after
def multiply(a, b):
  print(a * b)

multiply(5, 10)
```

    Before multiply
    50
    After multiply



```python

```
