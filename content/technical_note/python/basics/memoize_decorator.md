---
title: "Useful decorators: Memoizing, timer, type check"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Timer decorator
Time your functions!


```python
from functools import wraps
import time
def timer(func):
    """ A decorator that prints how long a function took to run"""
    # define the wrapper function to return 
    @wraps(func)
    def wrapper(*args, **kwargs):
        # When wrapper() is called, get current time
        t_start = time.time()
        # Call the decorated function and store the result
        result = func(*args, **kwargs)
        # Get the total time it took to run, and print it
        t_total = time.time() - t_start
        print(f'{func.__name__} took {t_total}s')
        return result
    
    return wrapper
```

### Memoize
Store results of functions for fast lookup so that the function runs faster the second time a function is called with the same arguments.


```python
from functools import wraps
def memoize(func):
    """Store the results of the decorated function for fast lookup"""
    # Store results in a dict that maps arguments to results
    cache = {}
    # Define the wrapper function to return.
    @wraps(func)
    def wrapper(*args,**kwargs):
        # If these arguments haven't been seen before,
        key = str(args) + str(kwargs)
        if key not in cache:
            # Call func() and store the result.
            cache[key] = func(*args,**kwargs)
        return cache[key]
    return wrapper
```


```python
@timer
@memoize
def multiply_slow(a,b):
    time.sleep(5)
    return a*b
```


```python
# here the call runs slowly
multiply_slow(1,2)
```

    wrapper took 5.003448247909546s





    2




```python
# here the calls runs much faster
multiply_slow(1,2)
```

    wrapper took 5.7220458984375e-06s





    2



### Check type
Examine the results of your functions at runtime by checking the type returned.


```python
from functools import wraps
def print_return_type(func):# Define wrapper(), the decorated function
  @wraps(func)
  def wrapper(*args, **kwargs):
    # Call the function being decorated
    result = func(*args, **kwargs)
    print('{}() returned type {}'.format(
      func.__name__, type(result)
    ))
    return result
  # Return the decorated function
  return wrapper
  
@print_return_type
def foo(value):
  return value
  
print(foo(42))
print(foo([1, 2, 3]))
print(foo({'a': 42}))
```

    foo() returned type <class 'int'>
    42
    foo() returned type <class 'list'>
    [1, 2, 3]
    foo() returned type <class 'dict'>
    {'a': 42}


### Counter
decorator that adds a counter to each function that you decorate. decorate a bunch of functions with the counter() decorator, let your program run for a while, and then print out how many times each function was called.



```python
from functools import wraps
def counter(func):
  @wraps(func)
  def wrapper(*args, **kwargs):
    wrapper.count += 1
    # Call the function being decorated and return the result
    return func(*args, **kwargs)
  wrapper.count = 0
  # Return the new decorated function
  return wrapper

# Decorate foo() with the counter() decorator
@counter
def foo():
  print('calling foo()')
  
foo()
foo()

print('foo() was called {} times.'.format(foo.count))
```

    calling foo()
    calling foo()
    foo() was called 2 times.


### Measuring decorator overhead
Access the original function using wraps attribute `__wrapped__`


```python
import time
from functools import wraps

def check_everything(func):
  @wraps(func)
  def wrapper(*args, **kwargs):
    time.sleep(2)
    result = func(*args, **kwargs)
    return result
  return wrapper

@check_everything
def duplicate(my_list):
  """Return a new list that repeats the input twice"""
  return my_list + my_list

t_start = time.time()
duplicated_list = duplicate(list(range(50)))
t_end = time.time()
decorated_time = t_end - t_start

t_start = time.time()
# Call the original function instead of the decorated one
duplicated_list = duplicate.__wrapped__(list(range(50)))
t_end = time.time()
undecorated_time = t_end - t_start

print('Decorated time: {:.5f}s'.format(decorated_time))
print('Undecorated time: {:.5f}s'.format(undecorated_time))
```

    Decorated time: 2.00555s
    Undecorated time: 0.00025s



```python

```
