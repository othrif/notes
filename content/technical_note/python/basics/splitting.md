---
title: "Splitting strings"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Basic splitting


```python
str = "I am playing with;##9Strings () while testing \n how these randome ## chE@sracters worK;\nhere\\right ## there"
```

#### split(seperator,maxsplit=positions)


```python
str.split()
```




    ['I',
     'am',
     'playing',
     'with;##9Strings',
     '()',
     'while',
     'testing',
     'how',
     'these',
     'randome',
     '##',
     'chE@sracters',
     'worK;here\\right',
     '##',
     'there']




```python
str.split('##')
```




    ['I am playing with;',
     '9Strings () while testing \n how these randome ',
     ' chE@sracters worK;here\\right ',
     ' there']




```python
str.split('##',2)
```




    ['I am playing with;',
     '9Strings () while testing \n how these randome ',
     ' chE@sracters worK;here\\right ## there']




```python
str.split('##',maxsplit=2)
```




    ['I am playing with;',
     '9Strings () while testing \n how these randome ',
     ' chE@sracters worK;here\\right ## there']



#### rsplit(seperator,maxsplit=positions)


```python
str.rsplit('##',maxsplit=2)
```




    ['I am playing with;##9Strings () while testing \n how these randome ',
     ' chE@sracters worK;here\\right ',
     ' there']



#### Consecutive delimiters
Consecutive delimiters give empty strings


```python
str.rsplit('#')
```




    ['I am playing with;',
     '',
     '9Strings () while testing \n how these randome ',
     '',
     ' chE@sracters worK;here\\right ',
     '',
     ' there']




```python
'helo  ljdk lksd   klsd'.rsplit()
```




    ['helo', 'ljdk', 'lksd', 'klsd']




```python
'helo  ljdk lksd   klsd'.rsplit(' ')
```




    ['helo', '', 'ljdk', 'lksd', '', '', 'klsd']



#### Disasembling strings to lines


```python
str.splitlines()
```




    ['I am playing with;##9Strings () while testing ',
     ' how these randome ## chE@sracters worK;',
     'here\\right ## there']



Keep end of lines by passing `True`


```python
str.splitlines(True)
```




    ['I am playing with;##9Strings () while testing \n',
     ' how these randome ## chE@sracters worK;\n',
     'here\\right ## there']



### Partition
Split string at the first occurence of seperator, and return 3 tuple: (before sep, sep, after sep)


```python
'first;second;third'.partition(';')
```




    ('first', ';', 'second;third')



compare with


```python
'first;second;third'.split(';',1)
```




    ['first', 'second;third']


