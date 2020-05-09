---
title: "Manipulation, indexing, and slicing"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Access elements


```python
txt = 'Hello world!'
```


```python
txt[0]
```




    'H'




```python
txt[4]
```




    'o'



### Substrings


```python
txt[0:5]
```




    'Hello'



### Backwards


```python
txt[-1]
```




    '!'




```python
txt[-5]
```




    'o'



### Skip over


```python
txt[::2]
```




    'Hlowrd'



### Reverse


```python
txt[::-1]
```




    '!dlrow olleH'



### Concatenation


```python
language = 'Python'
language + ' is great!'
```




    'Python is great!'



### Repetition


```python
'.'*100
```




    '....................................................................................................'




```python
100*'.'
```




    '....................................................................................................'



### Length


```python
len(language)
```




    6



### Escape Characters


```python
print('\N{GREEK CAPITAL LETTER DELTA}')
print('\u0394') # unicode 16-bit hex
print('\U00000394')# unicode 32-bit hex
```

    Δ
    Δ
    Δ


### Summary


```python
txt = 'Hello World'
print(f'Particular element: {txt[0]}')
print(f'substring: {txt[0:5]}')
print(f'substring: {txt[:5]}')
print(f'substring: {txt[0:-6]}')
print(f'substring: {txt[6:]}')
print(f'skip 2: {txt[::2]}')
print(f'skip 3: {txt[::3]}')
print(f'Invert order: {txt[::-1]}')
print(f'String length: {len(txt)}')
print(f'Repetition: {"."*10}')
print(f'Concatenation: {txt+" from Hamburg!"}')
print(f'Escape characters...')
print(f'few examples in this line: \'\"123\b \thorizontal')
print(f'1234567 carriage return \rXXX')
```

    Particular element: H
    substring: Hello
    substring: Hello
    substring: Hello
    substring: World
    skip 2: HloWrd
    skip 3: HlWl
    Invert order: dlroW olleH
    String length: 11
    Repetition: ..........
    Concatenation: Hello World from Hamburg!
    Escape characters...
    few examples in this line: '"12 	horizontal
    XXX4567 carriage return 


### Strings are immutable


```python
language[9]=-1
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-45-4d8be7846d5d> in <module>
    ----> 1 language[9]=-1
    

    TypeError: 'str' object does not support item assignment


you cannot change the values inside of string


```python
~1


```




    -2


