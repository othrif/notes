---
title: "Hashing strings"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Hashing strings

A hash function is a function that takes input of a variable length sequence of bytes and converts it to a fixed length sequence.

You will need to pass byte encoding or encode string.

### Used to encode unique filenames 


```python
import hashlib
import uuid
for _ in range(3):
    filename = hashlib.sha1('myfile'.encode('utf-8')).hexdigest()[:8]+'_'+str(uuid.uuid4().hex)
    print(filename)
```

    b3580ab4_2aa33c2df5bc4f569d83d6924d04541c
    b3580ab4_7c170be56bd0466cac020e18189b842d
    b3580ab4_8e518d7fdffb4eb0bde3cfc0d7cec3dc


### Available algorithms


```python
import hashlib
print(hashlib.algorithms_available) # lists all the algorithms available in the system,
print(hashlib.algorithms_guaranteed) # only lists the algorithms present in the module
```

    {'sha1', 'sha3_256', 'sha3_224', 'shake_256', 'sha512_256', 'md5-sha1', 'blake2s', 'sha256', 'md4', 'md5', 'sm3', 'sha224', 'sha3_512', 'blake2b', 'sha512_224', 'sha3_384', 'ripemd160', 'sha512', 'sha384', 'mdc2', 'shake_128', 'whirlpool'}
    {'sha1', 'sha3_384', 'sha384', 'sha512', 'shake_128', 'blake2s', 'sha3_256', 'sha256', 'shake_256', 'md5', 'sha3_224', 'sha224', 'sha3_512', 'blake2b'}



```python
import hashlib
hash_object = hashlib.sha1(b'Hello World')
hex_dig = hash_object.hexdigest()
print(hex_dig)
```

    0a4d55a8d778e5022fab701977c5d840bbc486d0



```python
import hashlib
hash_object = hashlib.sha1('Hello World'.encode('utf-8'))
hex_dig = hash_object.hexdigest()
print(hex_dig)
```

    0a4d55a8d778e5022fab701977c5d840bbc486d0


### Shorten string


```python
hex_dig_short = hash_object.hexdigest()[:8]
print(hex_dig_short)
```

    0a4d55a8

