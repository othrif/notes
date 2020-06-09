---
title: "Lambda functions and map(), filter(), reduce()"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Basic syntax
``` python
lambda arguments : <do something>
```


```python
myfunc = lambda a: a+'!!!'
myfunc('hello')
```




    'hello!!!'



### Converting a function to lambda

Compare the two functions and how `lambda` is much more concise


```python
def echo_word_def(word1, echo):
    """Concatenate echo copies of word1."""
    words = word1 * echo
    return words
```


```python
echo_word_lambda = (lambda word1, echo: word1*echo)
```


```python
print(echo_word_def('hey',5))
print(echo_word_lambda('hey',5))
```

    heyheyheyheyhey
    heyheyheyheyhey


### `Map()` and lambda functions

map() applies a function over an object, such as a list. The syntax follows ` map(func, list)`


```python
nums = [2, 4, 6, 8, 10]

result = map(lambda a: a ** 2, nums)
```

in this example, a lambda function, which raises a value `a` to the power of 2, is passed to `map()` alongside a list of numbers, `nums`


```python
list(result)
```




    [4, 16, 36, 64, 100]



### `Filter()` and lambda functions

The function `filter()` offers a way to filter out elements from a list that don't satisfy certain criteria.


```python
fellowship = ['frodo', 'samwise', 'merry', 'pippin', 'aragorn', 'boromir', 'legolas', 'gimli', 'gandalf']
result = filter(lambda a: len(a)>6, fellowship)
result_list = list(result)
print(result_list)
```

    ['samwise', 'aragorn', 'boromir', 'legolas', 'gandalf']


### `Reduce()` and lambda functions

The `reduce()` function is useful for performing some computation on a list and, unlike `map()` and `filter()`, returns a single value as a result. To use reduce(), you must import it from the functools module.


```python
from functools import reduce 
```


```python
stark = ['robb', 'sansa', 'arya', 'brandon', 'rickon']
result = reduce(lambda item1,item2: item1+item2 , stark)
print(result)
```

    robbsansaaryabrandonrickon

