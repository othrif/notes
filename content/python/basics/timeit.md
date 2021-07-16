---
title: "Time and profile your code"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Using timeit
`timeit.timeit` function only accepts strings. This can be quite annoying if you want to measure larger functions.


```python
import timeit
timeit.timeit('"-".join(str(n) for n in range(10_000_000))', number=1)
```




    2.7127743320000093



### Using context manager


```python
from contextlib import contextmanager
from time import time


@contextmanager
def timing(description: str) -> None:
    start = time()
    yield
    ellapsed_time = time() - start

    print(f"{description}: {ellapsed_time}")


with timing("List Comprehension Example"):
    s = [x for x in range(10_000_000)]
```

    List Comprehension Example: 0.5566189289093018


### Using class


```python
from time import time

class TimeTook(object):
    """
    Calculates the time a block took to run.
    Example usage:
    with TimeTook("sample"):
        s = [x for x in range(10000000)]
    """
    def __init__(self, description):
        self.description = description

    def __enter__(self):
        self.start = time()

    def __exit__(self, type, value, traceback):
        self.end = time()
        print(f"Time took for {self.description}: {self.end - self.start}")
        
with TimeTook("List Comprehension Example"):
    s = [x for x in range(10_000_000)]
```

    Time took for List Comprehension Example: 0.5780296325683594


### Using SnakeViz

### CLI

``` bash 
python -m cProfile -o program.prof my_program.py
snakeviz program.prof
```

### IPython
``` bash 
%prun -D program.prof glob.glob('*.txt')
```

### Single line


```python
import glob
%load_ext snakeviz
%snakeviz glob.glob('*.*')
```

    The snakeviz extension is already loaded. To reload it, use:
      %reload_ext snakeviz
     
    *** Profile stats marshalled to file '/var/folders/wn/k3vlc_7s4mjcszy_1l54z5qm0000gn/T/tmpxau65ynn'. 
    Embedding SnakeViz in this document...




<iframe id='snakeviz-716bc7d2-a1e0-11eb-8d18-acde48001122' frameborder=0 seamless width='100%' height='1000'></iframe>
<script>document.getElementById("snakeviz-716bc7d2-a1e0-11eb-8d18-acde48001122").setAttribute("src", "http://" + document.location.hostname + ":8080/snakeviz/%2Fvar%2Ffolders%2Fwn%2Fk3vlc_7s4mjcszy_1l54z5qm0000gn%2FT%2Ftmpxau65ynn")</script>



#### Multiple lines


```python
%%snakeviz
files = glob.glob('*.txt')
for file in files:
    with open(file) as f:
        print(hashlib.md5(f.read().encode('utf-8')).hexdigest())
```

     
    *** Profile stats marshalled to file '/var/folders/wn/k3vlc_7s4mjcszy_1l54z5qm0000gn/T/tmpc8imb63p'. 
    Embedding SnakeViz in this document...




<iframe id='snakeviz-77eca5cc-a1e0-11eb-8d18-acde48001122' frameborder=0 seamless width='100%' height='1000'></iframe>
<script>document.getElementById("snakeviz-77eca5cc-a1e0-11eb-8d18-acde48001122").setAttribute("src", "http://" + document.location.hostname + ":8080/snakeviz/%2Fvar%2Ffolders%2Fwn%2Fk3vlc_7s4mjcszy_1l54z5qm0000gn%2FT%2Ftmpc8imb63p")</script>




```python

```
