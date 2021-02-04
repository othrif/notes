---
title: "Primitive types"
date: 2021-02-04T00:00:00+00:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Definition

Everything in Python is an object. Primitive types are built-in types such as: numerics (integers,etc.), sequences (lists...), mappings (dict), classes, instances, and exceptions.

### Maximum of numerics


```python
# max integer is a function of the memory size
import sys
maxInt = sys.maxsize
print(maxInt, sys.maxsize==2**63-1) # 64-bit machine
```

    9223372036854775807 True



```python
# Bounds on floats
print(sys.float_info)
sys.float_info.max
```

    sys.float_info(max=1.7976931348623157e+308, max_exp=1024, max_10_exp=308, min=2.2250738585072014e-308, min_exp=-1021, min_10_exp=-307, dig=15, mant_dig=53, epsilon=2.220446049250313e-16, radix=2, rounds=1)





    1.7976931348623157e+308



### Bitwise operations


```python

```
