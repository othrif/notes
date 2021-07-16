---
title: "map, zip, eval, ord, dir, pow  function"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### map() 

The `map()` function allows you to execute a specified function for each item in an iterable that it takes as input(both function and iterable).

| Syntax: map(function, iterable)   


```python
def square(n):
    return n * n

num_list = [1,2,3,4]
result = map(square, num_list)
print('Mapped result is: ', list(result))
```

    Mapped result is:  [1, 4, 9, 16]


### zip()
If we pass two iterators in zip() function, both iterators containing the same number of elements, then the zip() function will return an iterator of a tuple. Each tuple contains a map of the same index elements from the given iterators.

| Syntax: zip(*iterators)


```python
numbers = [1, 2, 3]
letters = ['One', 'Two', 'Three']

result = zip(numbers, letters)

# converting values to print as set
result = set(result)
print('The zipped result is: ', result)
```

    The zipped result is:  {(1, 'One'), (3, 'Three'), (2, 'Two')}


### eval()

eval function evaluates a string input as a python expression and returns the output as an integer.

| Syntax : eval(string)


```python
result1 = eval('10 + 15')

result2 = eval('3 * 8')

print(result1)
print(result2)
```

    25
    24


### ord()

This function is used to return the Unicode code point of a given character.

| Syntax: ord(character)


```python
x = ord('a')
y = ord('$')
z = ord(' ')   #space character

print(x)
print(y)
print(z)
```

    97
    36
    32


#### dir()

`dir()` returns a valid list of all the attributes of the specified object.

|Syntax: dir(object)


```python
class Student:
  name = "Joy",
  age = 16,
  rollNo = 25
  
print(dir(Student))
```

    ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'age', 'name', 'rollNo']

