---
title: "Built-in object methods"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
# List of most widely used methods per object type
- Everything = object
- Objects have methods associated depending on type
- Unlike functions, methods are only called on an object (list, str, etc.)
- Methods can alter the object

## list methods
See all methods by typing `help(list)` and scroll down after `__...__`, you start seeing the methods

#### `index()`


```python
mylist = [1,2,'hello','othmane',2,3,4,'hello']
mylist.index('othmane')
```




    3



#### `count()`


```python
mylist.count('hello')
```




    2



#### `append()`


```python
mylist.append('really')
mylist
```




    [1, 2, 'hello', 'othmane', 2, 3, 4, 'hello', 'really']



#### `reverse()`


```python
# Create list areas
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

# Use append twice to add poolhouse and garage size
areas.append(24.5)
areas.append(15.45)

# Print out areas
print(areas)

# Reverse the orders of the elements in areas
areas.reverse()

# Print out areas
print(areas)
```

    [11.25, 18.0, 20.0, 10.75, 9.5, 24.5, 15.45]
    [15.45, 24.5, 9.5, 10.75, 20.0, 18.0, 11.25]


## str methods

#### `capitalize()`


```python
mystr = 'othmane'
mystr.capitalize()
```




    'Othmane'



#### `replace()`


```python
mystr.replace('h','H')
```




    'otHmane'



#### `index()`


```python
mystr.index('h')
```




    2




```python

```
