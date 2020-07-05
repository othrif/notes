---
title: "Timer decorator for how long a function took to run"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Timer decorator


```python
import time 

def timer(func):
    """ A decorator that prints how long a function took to run"""
    # define the wrapper function to return 
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


```python
@timer
def multiply(a,b):
    return a*b
```


```python
multiply(1,2)
```

    multiply took 1.1920928955078125e-06s





    2




```python
@timer
def sleep_n_seconds(n):
    time.sleep(n)
```


```python
sleep_n_seconds(5)
```

    sleep_n_seconds took 5.004380941390991s



```python
sleep_n_seconds(10)
```

    sleep_n_seconds took 10.002737045288086s

