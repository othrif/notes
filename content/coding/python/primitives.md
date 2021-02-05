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
# Bounds on ints
import sys
print(sys.int_info)
```

    sys.int_info(bits_per_digit=30, sizeof_digit=4)



```python
# Bounds on floats
print(sys.float_info)
sys.float_info.max
```

    sys.float_info(max=1.7976931348623157e+308, max_exp=1024, max_10_exp=308, min=2.2250738585072014e-308, min_exp=-1021, min_10_exp=-307, dig=15, mant_dig=53, epsilon=2.220446049250313e-16, radix=2, rounds=1)





    1.7976931348623157e+308



### Unicode, numbering systems


```python
# bin representation
0b11
```




    3




```python
# Octal representation
0o11
```




    9




```python
# Hex representation
0o11
```




    9




```python
# To binary
[bin(i) for i in [1, 2, 4, 8, 16]] 
```




    ['0b1', '0b10', '0b100', '0b1000', '0b10000']




```python
# From binary
[int(i, base=2) for i in ['0b1', '0b10', '0b100', '0b1000', '0b10000']] 
```




    [1, 2, 4, 8, 16]




```python
# To hex
[hex(i) for i in [1, 2, 4, 8, 16]]
```




    ['0x1', '0x2', '0x4', '0x8', '0x10']




```python
# To ordinal value
ord('a')
```




    97




```python
# From ordinal value
chr(97)
```




    'a'




```python
# to bytes (b'' is for bytes)
bytes((104, 101, 108, 108, 111, 32, 119, 111, 114, 108, 100))
```




    b'hello world'




```python
# encode using UTF-8
"résumé".encode("utf-8")
```




    b'r\xc3\xa9sum\xc3\xa9'




```python
# decode using UTF-8
b'r\xc3\xa9sum\xc3\xa9'.decode("utf-8")
```




    'résumé'



### Bitwise operations


```python
# Bitwise OR
bin(0b10101 | 0b01010)
```




    '0b11111'




```python
# Bitwise AND
bin(0b10101 & 0b11010)
```




    '0b10000'




```python
# Bitwise NOT (caution with negative sign in python)
bin(~0b10011100 & 255)
```




    '0b1100011'




```python
# Bitwise XOR (a_i + b_i mod 2)
bin(0b10101 ^ 0b01110)
```




    '0b11011'




```python
# Logical XOR (do not have equivalent similar to: & => and)
def xor(a, b):
    return (a and not b) or (not a and b)
xor(2>8, 1>0)
```




    True




```python
# Left shift (a << n = a x 2^n)
bin(0b100111 << 1)
```




    '0b1001110'




```python
print(f'{0b100111 << 1} is 2x {0b100111}')
```

    78 is 2x 39



```python
# restrict to 8 bytes = 2^8-1
39 << 3 & 255
```




    56




```python
# Right shift(a >> n = a // 2^n, // => floor division)
bin(0b100111 >> 1)
```




    '0b10011'




```python
print(5 >> 1, 5 // 2, 5/2)
```

    2 2 2.5



```python
# Sign bit
print(bin(-42), bin(42), sep="\n ")
```

    -0b101010
     0b101010



```python
mask = 0b11111111  # Same as 0xff or 255
bin(-42 & mask)
```




    '0b11010110'




```python
int('0b11010110', 2) # 214 in unsigned same as -42 in signed
```




    214




```python
# Bitmask: getting a bit
```


```python
# suppress all bitss except desired one: 2 ^ bit index
def get_bit(value, bit_index):
    return value & (1 << bit_index)
get_bit(0b10100000, bit_index=5)
```




    32




```python
# yes or no answer
def get_normalized_bit(value, bit_index):
    return (value >> bit_index) & 1
get_normalized_bit(0b10100000, bit_index=5)
```




    1




```python
# setting a bit
def set_bit(value, bit_index):
    return value | (1 << bit_index)
set_bit(0b10000000, bit_index=5)
```




    160




```python
# unsetting bit
def clear_bit(value, bit_index):
    return value & ~(1 << bit_index)
bin(clear_bit(0b11111111, bit_index=5))
```




    '0b11011111'




```python
# toggle bit on/off
def toggle_bit(value, bit_index):
    return value ^ (1 << bit_index)
x = 0b10100000
for _ in range(5):
    x = toggle_bit(x, bit_index=7)
    print(bin(x))
```

    0b100000
    0b10100000
    0b100000
    0b10100000
    0b100000



```python
# bitwise operator overloading
fruits = {"apple", "banana", "tomato"}
veggies = {"eggplant", "tomato"}
print(fruits | veggies)
print(fruits & veggies)
print(fruits ^ veggies)
print(fruits - veggies)
```

    {'tomato', 'banana', 'apple', 'eggplant'}
    {'tomato'}
    {'eggplant', 'apple', 'banana'}
    {'apple', 'banana'}

