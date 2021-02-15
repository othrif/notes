---
title: "Primitive types"
date: 2021-02-04T00:00:00+00:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Definition

Everything in Python is an object. Primitive types are built-in types such as: numerics (integers,etc.), sequences (lists...), mappings (dict), classes, instances, and exceptions.

### Key methods for numeric


```python
import math
print(f'Absolutve value: {abs(-34.5)}')
print(f'Round up: {math.ceil(34.5)}')
print(f'Round down: {math.floor(34.5)}')
print(f'Max value: {max(34.5, 1000)}')
print(f'Power: {pow(34.5,2)} OR {34.5**2}')
print(f'Square root: {math.sqrt(34.5)}')
```

    Absolutve value: 34.5
    Round up: 35
    Round down: 34
    Max value: 1000
    Power: 1190.25 OR 1190.25
    Square root: 5.873670062235365


### Interconvert numbers and strings


```python
str(42)
```




    '42'




```python
int('42')
```




    42




```python
str(87.3)
```




    '87.3'




```python
float('87.3')
```




    87.3



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
sys.float_info.max
```




    1.7976931348623157e+308




```python
# Pseudo max-float / min-float
print(f'Max float:{float("inf")}, Min float:{float("-inf")}')
print(f'Inf is larger than max int: {float("inf") > sys.maxsize}')
```

    Max float:inf, Min float:-inf
    Inf is larger than max int: True


### Best of random


```python
import random
# randrange([start], stop[, step])
print(f'randrange(start): {random.randrange(100)}') # 0 to 99 [0,100)
print(f'randrange(start, stop, step): {random.randrange(0, 100, 2)}') # 0 to 99 [0,100) with setps of 2
# randint(a, b) = randrange(a,b+1)
print(f'randint(start, stop): {random.randint(0,100)}') # 0 to 100 [0,100]
```

    randrange(start): 49
    randrange(start, stop, step): 58
    randint(start, stop): 27



```python
# Random float:  0.0 <= x < 1.0
print(f'random(): {random.random()}')
# Random float:  2.5 <= x < 10.0
print(f'uniform(): {random.uniform(2.5, 10.0)}')
```

    random(): 0.09094037940054844
    uniform(): 5.191762349159088



```python
# Randomly shuffle a lit
A = [1,2,3,4,5]
random.shuffle(A)
A
```




    [3, 4, 2, 1, 5]




```python
# Single random element from a sequence
random.choice(['win', 'lose', 'draw'])
```




    'lose'



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
0x11
```




    17




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
# To ordinal value (index of character in utf-8 or ascii)
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
# 255 = 2^8 -1
bin(~0b10011100 & 255)
```




    '0b1100011'




```python
# Function to perform bitwise not operation
def bit_not(n, numbits=8):
    return ~n & ((1 << numbits) - 1)
print(bin(bit_not(0b10011100)))

# Alternative formulation:
def bit_not(n, numbits=8):
    return (1 << numbits) - 1 - n
print(bin(bit_not(0b10011100)))
```

    0b1100011
    0b1100011



```python
# ~x = -x-1
~0
```




    -1




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
# restrict to 8 bits = 2^8-1
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
# Bitmask operations: 
# value OP (1 << bit_index)
# getting a bit => &
# setting a bit => |
# unsetting a bit => | ~
# toggling a bit => ^
```


```python
# getting a bit

# suppress all bits except desired one (2 ^ bit index)
def get_bit(value, bit_index):
    return value & (1 << bit_index)
print(get_bit(0b10100000, bit_index=5))

# yes or no answer
def get_normalized_bit(value, bit_index):
    return (value >> bit_index) & 1
print(get_normalized_bit(0b10100000, bit_index=5))
```

    32
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
# toggle a bit on/off
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


### Important notations
`a >>= b` means `a = a >> b`

### Important tricks


```python
# x & (x-1): erase the lowest set bit
print(bin(1833))
print(bin(1832))
print(bin(1833 & 1832))
```

    0b11100101001
    0b11100101000
    0b11100101000



```python
# x & ~(x-1): isolates the lowest set bit
print(bin(1833))
print(bin(1832))
print(bin(1833 & ~1832))
```

    0b11100101001
    0b11100101000
    0b1



```python
# Number of digits in a number
import math
math.floor(math.log10(12345))+1
```




    5




```python
# Get the least significant digit
12345 % 10
```




    5




```python
# Get the most significant digit
num_digits = math.floor(math.log10(12345))+1
mask = 10**(num_digits-1)
12345 // mask
```




    1


