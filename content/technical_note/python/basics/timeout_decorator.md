---
title: "Timeout decorator for a function that runs longer than expected"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Pass argument to decorator
Timeout decorator for a function that runs longer than expected


```python
import signal

def raise_timeout(*args, **kwargs):
    raise TimeoutError('This function has timed out!!!!!')

# When an "alarm" signal goes off, call raise_timeout()
signal.signal(signalnum=signal.SIGALRM, handler=raise_timeout)
# Set off an alarm in 5 seconds
signal.alarm(5)
# Cancel the alarm
signal.alarm(0)
raise_timeout()
```


    ---------------------------------------------------------------------------

    TimeoutError                              Traceback (most recent call last)

    <ipython-input-47-a751c17ccd28> in <module>
         10 # Cancel the alarm
         11 signal.alarm(0)
    ---> 12 raise_timeout()
    

    <ipython-input-47-a751c17ccd28> in raise_timeout(*args, **kwargs)
          2 
          3 def raise_timeout(*args, **kwargs):
    ----> 4     raise TimeoutError('This function has timed out!!!!!')
          5 
          6 # When an "alarm" signal goes off, call raise_timeout()


    TimeoutError: This function has timed out!!!!!



```python
from functools import wraps
import time 
def timeout(n_seconds):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            # Set an alarm for n seconds
            signal.alarm(n_seconds)
            try:
                # Call the decorated func
                return func(*args,**kwargs)
            finally:
                # Cancel alarm
                signal.alarm(0)
        return wrapper
    return decorator
```


```python
@timeout(5)
def foo():
    time.sleep(10)
    print('foo!')
```


```python
foo()
```


    ---------------------------------------------------------------------------

    TimeoutError                              Traceback (most recent call last)

    <ipython-input-50-c19b6d9633cf> in <module>
    ----> 1 foo()
    

    <ipython-input-48-d1ae5af212c1> in wrapper(*args, **kwargs)
          9             try:
         10                 # Call the decorated func
    ---> 11                 return func(*args,**kwargs)
         12             finally:
         13                 # Cancel alarm


    <ipython-input-49-b4a5c0804cd2> in foo()
          1 @timeout(5)
          2 def foo():
    ----> 3     time.sleep(10)
          4     print('foo!')


    <ipython-input-47-a751c17ccd28> in raise_timeout(*args, **kwargs)
          2 
          3 def raise_timeout(*args, **kwargs):
    ----> 4     raise TimeoutError('This function has timed out!!!!!')
          5 
          6 # When an "alarm" signal goes off, call raise_timeout()


    TimeoutError: This function has timed out!!!!!

