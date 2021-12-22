---
title: "Regular expressions"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Extremely useful to understand what the pattern means: https://regexr.com/

# `re.search()` pattern
``` python
match = re.search(pat, str)
```

### Basic patterns

* a, X, 9, < -- ordinary characters just match themselves exactly. Meta-characters don't: . ^ $ * + ? { [ ] \ | ( )   

* . (a period) -- matches any single character except newline '\n'    
* \w -- (lowercase w) matches a "word" character: a letter or digit or underbar [a-zA-Z0-9_].   
* \W (upper case W) matches any non-word character   
* \b -- boundary between word and non-word   
* \s -- (lowercase s) matches a single whitespace character. \S (upper case S) matches any non-whitespace character   
* \t, \n, \r -- tab, newline, return   
* \d -- decimal digit [0-9]   
* ^ = start, $ = end -- match the start or end of the string   
* \ -- inhibit the "specialness" of a character. So, for example, use \. to match a period or \\ to match a slash  


```python
import re
str = 'an example word:cat!!'
match = re.search(r'word:\w\w\w', str)
# If-statement after search() tests if it succeeded
if match:
  print('found', match.group())
else:
  print('did not find')
```

    found word:cat



```python
re.search(r'iii', 'piiig').group()
```




    'iii'




```python
re.search(r'..g', 'piiig')
```




    <re.Match object; span=(2, 5), match='iig'>




```python
re.search(r'\d\d\d', 'p123g')
```




    <re.Match object; span=(1, 4), match='123'>




```python
re.search(r'\w\w\w', '@@abcd!!') 
```




    <re.Match object; span=(2, 5), match='abc'>



### Repetition

First the search finds the leftmost match for the pattern, and second it tries to use up as much of the string as possible

* \+ -- 1 or more occurrences of the pattern to its left, e.g. 'i+' = one or more i's
* \* -- 0 or more occurrences of the pattern to its left
* \? -- match 0 or 1 occurrences of the pattern to its left



```python
re.search(r'pi+', 'piiig')
```




    <re.Match object; span=(0, 4), match='piii'>




```python
re.search(r'i+', 'piigiiii')
```




    <re.Match object; span=(1, 3), match='ii'>




```python
re.search(r'\d\s*\d\s*\d', 'xx1 2   3xx')
```




    <re.Match object; span=(2, 9), match='1 2   3'>




```python
re.search(r'b\w+', 'foobar')
```




    <re.Match object; span=(3, 6), match='bar'>



### Square Brackets

[abc] matches 'a' or 'b' or 'c'.


```python
str = 'purple alice-b@google.com monkey dishwasher'
match = re.search(r'[\w.-]+@[\w.-]+', str)
if match:
  print(match.group())
```

    alice-b@google.com


### Group Extraction


```python
str = 'purple alice-b@google.com monkey dishwasher'
match = re.search(r'([\w.-]+)@([\w.-]+)', str)
if match:
  print(match.group())  ## 'alice-b@google.com' (the whole match)
  print(match.group(1))  ## 'alice-b' (the username, group 1)
  print(match.group(2))  ## 'google.com' (the host, group 2)
```

    alice-b@google.com
    alice-b
    google.com


# `findall`

`re.search()` to find the first match for a pattern. `findall()` finds **all** the matches and returns them as a list of strings


```python
  ## Suppose we have a text with many email addresses
  str = 'purple alice@google.com, blah monkey bob@abc.com blah dishwasher'

  ## Here re.findall() returns a list of all the found email strings
  emails = re.findall(r'[\w\.-]+@[\w\.-]+', str) ## ['alice@google.com', 'bob@abc.com']
  for email in emails:
    # do something with each found email string
    print(email)
```

    alice@google.com
    bob@abc.com


#### `findall` with files

```python
# Open file
f = open('test.txt', 'r')
# Feed the file text into findall(); it returns a list of all the found strings
strings = re.findall(r'some pattern', f.read())
```

#### `findall` and groups
Using the parenthesis () group mechanism.


```python
str = 'purple alice@google.com, blah monkey bob@abc.com blah dishwasher'
tuples = re.findall(r'([\w\.-]+)@([\w\.-]+)', str)
print (tuples)  ## [('alice', 'google.com'), ('bob', 'abc.com')]
for tuple in tuples:
  print (tuple[0])  ## username
  print (tuple[1])  ## host
```

    [('alice', 'google.com'), ('bob', 'abc.com')]
    alice
    google.com
    bob
    abc.com


### Use of `?` and `^` for greedy vs non-greedy


```python
str = '<b>foo</b> and <i>so on</i>' 
re.search(r'<.*>', str)
```




    <re.Match object; span=(0, 27), match='<b>foo</b> and <i>so on</i>'>




```python
re.findall(r'<.*?>', str)
```




    ['<b>', '</b>', '<i>', '</i>']




```python
re.findall(r'[^>]*', str)
```




    ['<b', '', 'foo</b', '', ' and <i', '', 'so on</i', '', '']



# Substiution 

``` python
re.sub(pat, replacement, str)
```
The function searches for all the instances of pattern in the given string, and replaces them.


```python
  str = 'purple alice@google.com, blah monkey bob@abc.com blah dishwasher'
  ## re.sub(pat, replacement, str) -- returns new string with all replacements,
  ## \1 is group(1), \2 group(2) in the replacement
  print (re.sub(r'([\w\.-]+)@([\w\.-]+)', r'\1@yo-yo-dyne.com', str))
```

    purple alice@yo-yo-dyne.com, blah monkey bob@yo-yo-dyne.com blah dishwasher


# Non-capturing group


```python
re.findall(r'(?:ha)+', 'hahaha haa hah!')
```




    ['hahaha', 'ha', 'ha']




```python
re.findall(r'(ha)+', 'hahaha haa hah!')
```




    ['ha', 'ha', 'ha']




```python

```
