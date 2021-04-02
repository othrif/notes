---
title: "Tuple and namedtuple"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Tuple
The standard tuple uses numerical indexes to access its members. 


```python
bob = ('Bob', 30, 'male')
print(f'Representation:{bob}')

jane = ('Jane', 29, 'female')
print(f'\nField by index: {jane[0]}')

print('\nFields by index:')
for p in [ bob, jane ]:
    print('%s is a %d year old %s' % p)
```

    Representation:('Bob', 30, 'male')
    
    Field by index: Jane
    
    Fields by index:
    Bob is a 30 year old male
    Jane is a 29 year old female


### Namedtuple
remembering which index should be used for each value can lead to errors. A namedtuple assigns names, as well as the numerical index, to each member.


```python
import collections

Person = collections.namedtuple('Person', 'name age gender')

print('Type of Person:', type(Person))

bob = Person(name='Bob', age=30, gender='male')
print('\nRepresentation:', bob)

jane = Person(name='Jane', age=29, gender='female')
print('\nField by name:', jane.name)

print('\nFields by index:')
for p in [ bob, jane ]:
    print('%s is a %d year old %s' % p)
```

    Type of Person: <class 'type'>
    
    Representation: Person(name='Bob', age=30, gender='male')
    
    Field by name: Jane
    
    Fields by index:
    Bob is a 30 year old male
    Jane is a 29 year old female


### Used inside classes


```python
class Stack:

    ElementCached = collections.namedtuple('ElementCached', ('element', 'max'))

    def __init__(self) -> None:
        self._elementcached_max: List[Stack.ElementCached] = []
    
    def push(self, x: int) -> None:

        self._elementcached_max.append(
            Stack.ElementCached(x, x if self.empty() else max(x, self.max()))
        )
```
