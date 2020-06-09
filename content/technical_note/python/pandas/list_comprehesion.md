---
title: "List comprehesion"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### List comprehesion
``` python 
[output expression for iterator variable in iterable]
```


```python
doctor = ['house', 'cuddy', 'chase', 'thirteen', 'wilson']
new_doctor = [doc[0] for doc in doctor]
print(new_doctor)
```

    ['h', 'c', 'c', 't', 'w']



```python
squares = [i**2 for i in range(10)]
print(squares)
```

    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]


### Nested list comprehesion
``` python
[[output expression] for iterator variable in iterable]
```


```python
# Create a 5 x 5 matrix using a list of lists
matrix = [[col for col in range(5)] for row in range(5)]
print(matrix)
```

    [[0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4], [0, 1, 2, 3, 4]]


### Conditional list comprehesion
``` python
[ output expression for iterator variable in iterable if predicate expression ].
```


```python
# Create a list of strings: fellowship
fellowship = ['frodo', 'samwise', 'merry', 'aragorn', 'legolas', 'boromir', 'gimli']

# Create list comprehension: new_fellowship
new_fellowship = [fellow for fellow in fellowship if len(fellow)>=7]

# Print the new list
print(new_fellowship)

```

    ['samwise', 'aragorn', 'legolas', 'boromir']


### if-else conditional on output expression
In the previous example, you used an if conditional statement in the predicate expression part of a list comprehension to evaluate an iterator variable. In this exercise, you will use an if-else statement on the output expression of the list.

``` python
[ output expression true if condition else output expression false for iterator variable in iterable if predicate expression ].
```


```python
# Create a list of strings: fellowship
fellowship = ['frodo', 'samwise', 'merry', 'aragorn', 'legolas', 'boromir', 'gimli']

# Create list comprehension: new_fellowship
new_fellowship = [member if len(member)>=7 else '' for member in fellowship]

# Print the new list
print(new_fellowship)

```

    ['', 'samwise', '', 'aragorn', 'legolas', 'boromir', '']

