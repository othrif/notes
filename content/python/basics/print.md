---
title: "Print statements"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### f-string formatting:
``` python
f ' <text> { <expression> <optional !s, !r, or !a> <optional : format specifier> } <text> ... '
```
where `<optional !s, !r, or !a>` mean `!s (str), !r (repr), and !a (ascii)`



```python
import datetime
name = 'Othmane'
age = 30
anniversary = datetime.date(1989, 2, 6)
print(f'My name is {name.lower()}, my age next year is {age+1}, my anniversary is {anniversary:%A, %B %d, %Y}.')
print(f'He said his name is {name!r}.') # !r for repr
print(r'Raw output: /Users/othmanerifki') # r for raw output
message = (
    f'Hi {name}.'
    f'Your age is {age}.'
)
print(message)
```

    In lower case:  othmane
    My name is othmane, my age next year is 31, my anniversary is Monday, February 06, 1989.
    He said his name is 'Othmane'.
    Raw output: /Users/othmanerifki
    Hi Othmane.Your age is 30.


### Quotation, braces:


```python
print(f'Using quotation {name}.')
print(f'Using quotation "{name}".')
print(f'Using quotation \'{name}\'.')
print(f'Without braces {74}')
print(f'With braces {{74}}')
print(f'to show more {{{{74}}}}')
```

    Using quotation Othmane.
    Using quotation "Othmane".
    Using quotation 'Othmane'.
    Without braces 74
    With braces {74}
    to show more {{74}}


### Number formatting
``` python f'{value:{width}.{precision}<type>}' ```  
`<type>`: s(string), f(float), d(decimal), x(hex), X(HEX), e(exponent scientific notation), E(same as e with 'E'), g(general, it rounds and format to scientific or fixed decimals), G(same as g but E), %(x100 and percent sign)


```python
weight = 83.1
print(f'With float is {weight:.2f}kg')
print(f'With percentage is {20/100:.2%}')
print(f'With scientific notation is {10**-6:.2E}')
print(f'With general notation is {10**-6:g}')
```

    With float is 83.10kg
    With percentage is 20.00%
    With scientific notation is 1.00E-06
    With general notation is 1e-06


### Indexing 
Not quite about printing, but a good illustration of what to expect


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


### Casting
Same as above, not related to printing but gives a good illustration


```python
x="10"
y="7.1"
print(f'Test with x+y where x={x}, y={y}')
print(f'No casting: x+y={x+y}')
print(f'Casting to float: x+y={float(x)+float(y)}')
print(f'Casting to int: x+y={int(x)+int(float(y))}') # int(7.1) give error
```

    Test with x+y where x=10, y=7.1
    No casting: x+y=107.1
    Casting to float: x+y=17.1
    Casting to int: x+y=17

