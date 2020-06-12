---
title: "Secant method"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Root-finding algorithm that has $(1+\sqrt{5})/2$ convergence.


```python
def secant_method(f, x0, x1, iterations):
    """Return the root calculated using the secant method."""
    for i in range(iterations):
        x2 = x1 - f(x1) * (x1 - x0) / float(f(x1) - f(x0))
        x0, x1 = x1, x2
    return x2

def f_example(x):
    return x**2 - 612

root = secant_method(f_example, 10, 30, 5)

print("Root: {}".format(root))  # Root: 24.738633748750722
```

    Root: 24.738633748750722



```python

```
