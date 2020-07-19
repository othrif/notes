---
title: "Iterables with enumerate() and zip()"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Big O notation
Say we have a certain algorithm. We run it on a modest number of fifty elements.
* O(1): One operation.
* O(log n): Four operations.
* O(n): Fifty operations.
* O(n log n): One hundred ninety-five operations.
* O(n²): Two thousand, five hundred operations.
* O(2^n): 1e15
* O(n!): 3e64



```python
import math

def computeBigO(functions, elements):
    operations = [[] for fn in functions]
    for e in elements:
        for n,fn in enumerate(functions):
            operations[n].append(fn(e))
    return operations

def O_log_n(n): return math.log(n)
def O_n(n): return n
def O_n_log_n(n): return n * math.log(n)
def O_n_2(n): return n * n
def O_2_n(n): return 2 ** n
def O_n_factorial(n): return math.factorial(n)

functions = [O_log_n, O_n, O_n_log_n, O_n_2, O_2_n, O_n_factorial]
scores = computeBigO(functions, range(1, 51))
for n,fn in enumerate(functions):
    print('%s:%s' % (fn, int(scores[n][-1])))
```

    <function O_log_n at 0x1065f8840>:3
    <function O_n at 0x110630598>:50
    <function O_n_log_n at 0x110630b70>:195
    <function O_n_2 at 0x110630f28>:2500
    <function O_2_n at 0x110630ea0>:1125899906842624
    <function O_n_factorial at 0x110630e18>:30414093201713378043612608166064768844377641568960512000000000000



```python
import matplotlib.pyplot as plt

col = ['yellow', 'orange', 'red', 'blue', 'violet', 'green']
for n,s in enumerate(scores):
    plt.plot(s,c=col[n])
    plt.ylim(0,500)
    plt.legend(['O($\log(n)$)','O($n$)','O($n\log(n)$)','O($n^2$)','O($2^n$)','O($n!$)'])
```


![png](bigO_3_0.png)

