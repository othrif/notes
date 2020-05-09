---
title: "Operators"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Bitwise operation


```python
x=3
```


```python
print(bin(x))
print(bin(~x))
~x # = -(x+1)
```

    0b11
    -0b100





    -4




```python
print(bin(6))
print(bin(3))
print(bin(6 | 3))
6 | 3
```

    0b110
    0b11
    0b111





    7



### Bitwise XOR
each position is 1 if only the first bit is 1 or only the second bit is 1, but will be 0 if both are 0 or both are 1


```python
print(bin(6))
print(bin(3))
print(bin(6 ^ 3))
6 ^ 3

```

    0b110
    0b11
    0b101





    5



use XOR as a short-cut to setting the value of a register to zero


```python
6 ^ 6
```




    0



### Shift operators


```python
print(bin(1))
print(bin(1 << 5))
```

    0b1
    0b100000



```python
print(bin(5))
print(bin(5 << 1))
print(5 << 1)
```

    0b101
    0b1010
    10



```python
print(bin(2))
print(bin(2 << 3))
print(2 << 3)
```

    0b10
    0b10000
    16



```python

```
