---
title: "Binary, Octal, and Hexadecimal Integers"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
# Summary table


```python
print(f'{"Decimal":<10} {"Binary":<15} {"Hexadecimal":<10}')
for i in range(32):
    i_bin = bin(i)
    i_oct = oct(i)
    i_hex = hex(i)
    print(f'{i:10} {i_bin:15} {i_hex:10}')
for i in range(5,10):
    i = 2**i
    i_bin = bin(i)
    i_oct = oct(i)
    i_hex = hex(i)
    print(f'{i:10} {i_bin:15} {i_hex:10}')
```

    Decimal    Binary          Hexadecimal
             0 0b0             0x0       
             1 0b1             0x1       
             2 0b10            0x2       
             3 0b11            0x3       
             4 0b100           0x4       
             5 0b101           0x5       
             6 0b110           0x6       
             7 0b111           0x7       
             8 0b1000          0x8       
             9 0b1001          0x9       
            10 0b1010          0xa       
            11 0b1011          0xb       
            12 0b1100          0xc       
            13 0b1101          0xd       
            14 0b1110          0xe       
            15 0b1111          0xf       
            16 0b10000         0x10      
            17 0b10001         0x11      
            18 0b10010         0x12      
            19 0b10011         0x13      
            20 0b10100         0x14      
            21 0b10101         0x15      
            22 0b10110         0x16      
            23 0b10111         0x17      
            24 0b11000         0x18      
            25 0b11001         0x19      
            26 0b11010         0x1a      
            27 0b11011         0x1b      
            28 0b11100         0x1c      
            29 0b11101         0x1d      
            30 0b11110         0x1e      
            31 0b11111         0x1f      
            32 0b100000        0x20      
            64 0b1000000       0x40      
           128 0b10000000      0x80      
           256 0b100000000     0x100     
           512 0b1000000000    0x200     


### Convert to Binary 


```python
a = 79
# Base 2(binary)
bin_a = bin(a)
print(bin_a)
print(int(bin_a, 2)) #Base 2(binary)
```

    0b1001111
    79


### Convert to Octal 


```python
a = 79
# Base 8(octal)
oct_a = oct(a)
print(oct_a)
print(int(oct_a, 8))
```

    0o117
    79


### Convert to Hexadecimal


```python
a = 79
# Base 16(hexadecimal)
hex_a = hex(a)
print(hex_a)
print(int(hex_a, 16))
```

    0x4f
    79



```python

```
