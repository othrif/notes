---
title: "Iterables with enumerate() and zip()"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Using `enumerate()`
`enumerate()` returns an enumerate object that produces a sequence of tuples, and each of the tuples is an index-value pair.


```python
mutants = ['charles xavier', 
            'bobby drake', 
            'kurt wagner', 
            'max eisenhardt', 
            'kitty pryde']

# Create a list of tuples
mutant_list = list(enumerate(mutants))
print(mutant_list)

# Unpack and print the tuple pairs
for index1,value1 in enumerate(mutants):
    print(index1, value1)

# Change the start index
for index2,value2 in enumerate(mutants, start=1):
    print(index2, value2)

```

    [(0, 'charles xavier'), (1, 'bobby drake'), (2, 'kurt wagner'), (3, 'max eisenhardt'), (4, 'kitty pryde')]
    0 charles xavier
    1 bobby drake
    2 kurt wagner
    3 max eisenhardt
    4 kitty pryde
    1 charles xavier
    2 bobby drake
    3 kurt wagner
    4 max eisenhardt
    5 kitty pryde


### Using `zip()`
takes any number of iterables and returns a zip object that is an iterator of tuples. If you wanted to print the values of a zip object, you can convert it into a list and then print it. Printing just a zip object will not return the values unless you unpack it first.


```python
mutants=['charles xavier', 'bobby drake', 'kurt wagner', 'max eisenhardt', 'kitty pryde']
aliases=['prof x', 'iceman', 'nightcrawler', 'magneto', 'shadowcat']
powers=['telepathy', 'thermokinesis', 'teleportation', 'magnetokinesis', 'intangibility']
```


```python
# Create a list of tuples
mutant_data = list(zip(mutants,aliases,powers))
print(mutant_data)

# Create a zip object using the three lists
mutant_zip = zip(mutants,aliases,powers)
print(mutant_zip)

# Unpack the zip object and print the tuple values
for value1,value2,value3 in mutant_zip:
    print(value1, value2, value3)
```

    [('charles xavier', 'prof x', 'telepathy'), ('bobby drake', 'iceman', 'thermokinesis'), ('kurt wagner', 'nightcrawler', 'teleportation'), ('max eisenhardt', 'magneto', 'magnetokinesis'), ('kitty pryde', 'shadowcat', 'intangibility')]
    <zip object at 0x10ac88b88>
    charles xavier prof x telepathy
    bobby drake iceman thermokinesis
    kurt wagner nightcrawler teleportation
    max eisenhardt magneto magnetokinesis
    kitty pryde shadowcat intangibility


### Using * and zip to 'unzip'
`*` unpacks an iterable such as a list or a tuple into positional arguments in a function call.


```python
# Create a zip object from mutants and powers
z1 = zip(mutants,powers)

# Print the tuples in z1 by unpacking with *
print(*z1)

# Re-create a zip object from mutants and powers, as the print(*) exhausted all elements of z1
z1 = zip(mutants,powers)

# 'Unzip' the tuples in z1 by unpacking with * and zip(): result1, result2
result1, result2 = zip(*z1)

# Check if unpacked tuples are equivalent to original tuples
print(result1 == mutants)
print(result2 == powers)

```

    ('charles xavier', 'telepathy') ('bobby drake', 'thermokinesis') ('kurt wagner', 'teleportation') ('max eisenhardt', 'magnetokinesis') ('kitty pryde', 'intangibility')
    False
    False

