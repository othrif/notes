---
title: "Class-level attributes, alternative constructors, and inheritance of class methods"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Class level attributes store data that is shared among all the class instances. They are assigned values in the class body and are refered to using the `ClassName` rather than `self` syntax  

### Class-level data
use `ClassName.ATTR_NAME` to accessthe class attribute value


```python
class Player:
    MAX_POSITION = 10
    MAX_SPEED = 3
    
    def __init__(self):
        self.position = 0

    # Add a move() method with steps parameter
    def move(self, steps):
        self.position += steps
        if self.position >= Player.MAX_POSITION:
            self.position = Player.MAX_POSITION
       
    # This method provides a rudimentary visualization in the console    
    def draw(self):
        drawing = "-" * self.position + "|" +"-"*(Player.MAX_POSITION - self.position)
        print(drawing)

p = Player(); p.draw()
p.move(4); p.draw()
p.move(5); p.draw()
p.move(3); p.draw()
```

    |----------
    ----|------
    ---------|-
    ----------|






```python
p1, p2 = Player(), Player()

print("MAX_SPEED of p1 and p2 before assignment:")
print(p1.MAX_SPEED)
print(p2.MAX_SPEED)

# Modify class attribute
Player.MAX_SPEED = 7

print("MAX_SPEED of p1 and p2 after assignment of class attribute:")
print(p1.MAX_SPEED)
print(p2.MAX_SPEED)
print("MAX_SPEED of Player:")
print(Player.MAX_SPEED)

# Modify instance attribute
p1.MAX_SPEED = 0

print("MAX_SPEED of p1 and p2 after assignment of instance attribute:")
print(p1.MAX_SPEED)
print(p2.MAX_SPEED)
print("MAX_SPEED of Player:")
print(Player.MAX_SPEED)


```

    MAX_SPEED of p1 and p2 before assignment:
    7
    7
    MAX_SPEED of p1 and p2 after assignment of class attribute:
    7
    7
    MAX_SPEED of Player:
    7
    MAX_SPEED of p1 and p2 after assignment of instance attribute:
    0
    7
    MAX_SPEED of Player:
    7


### Alternative constructors
Define class methods as well, using the `@classmethod` decorator and a special first argument cls. The main use of class methods is defining methods that return an instance of the class, but aren't using the same code as `__init__()`.


```python
# import datetime from datetime
from datetime import datetime

class BetterDate:
    def __init__(self, year, month, day):
      self.year, self.month, self.day = year, month, day
      
    @classmethod
    def from_str(cls, datestr):
        year, month, day = map(int, datestr.split("-"))
        return cls(year, month, day)
        
    # Define a class method from_datetime accepting a datetime object
    @classmethod
    def from_datetime(cls, datetime):
        return cls(datetime.year, datetime.month, datetime.day)
```


```python
bd_def = BetterDate(2020,7,3)   
print(bd_def.year)
print(bd_def.month)
print(bd_def.day)
```

    2020
    7
    3



```python
bd_str = BetterDate.from_str("2020-7-3")   
print(bd_str.year)
print(bd_str.month)
print(bd_str.day)
```

    2020
    7
    3



```python
today = datetime.today()     
bd = BetterDate.from_datetime(today)   
print(bd.year)
print(bd.month)
print(bd.day)
```

    2020
    7
    3


### Inheritance of class methods
To customize the parent's class method in a child class, start with a `@classmethod` decorator, and define a method with the same name in the child's class, just like you did with regular methods.

The only difference is that to call the parent's class method within the child's method, you can use `ClassName.method_name(args...)` without passing `self` or `cls`.


```python
# Define an EvenBetterDate class and customize from_str
class EvenBetterDate(BetterDate):
    @classmethod
    def from_str(self, datestr, format='YYYY-MM-DD'):
        if format=='YYYY-MM-DD':
            return BetterDate.from_str(datestr)
        elif format == 'DD-MM-YYYY':
            day,month,year = datestr.split('-')
            return BetterDate.from_str(('-').join([year, month, day]))
```


```python
ebd_str = EvenBetterDate.from_str('02-12-2019', format='DD-MM-YYYY')
print(ebd_str.year)
ebd_dt = EvenBetterDate.from_datetime(datetime.today())
print(ebd_dt.year)
```

    2019
    2020

