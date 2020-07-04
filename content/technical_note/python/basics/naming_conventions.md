---
title: "Attribute naming conventions"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### `_name`
A convention for internal details of implementation.
A helper method that checks the validity of an attribute's value but isn't considered a part of class's public interface.

 if you see an attribute name with one leading underscore in someone's class - don't use it! The class developer trusts you with this responsibility.


```python
# MODIFY to add class attributes for max number of days and months
class BetterDate:
  
    _MAX_DAYS = 30
    _MAX_MONTH = 12
    
    def __init__(self, year, month, day):
      self.year, self.month, self.day = year, month, day
      
    @classmethod
    def from_str(cls, datestr):
        year, month, day = map(int, datestr.split("-"))
        return cls(year, month, day)
    
    # Add _is_valid() checking day and month values
    def _is_valid(self):
        if self.day <= BetterDate._MAX_DAYS and self.month <= BetterDate._MAX_MONTH:
            return True
        else:
            return False
         
bd1 = BetterDate(2020, 4, 30)
print(bd1._is_valid())

bd2 = BetterDate(2020, 6, 45)
print(bd2._is_valid())
```

    True
    False


### `__name`
Used for attributes that should not be inherited to aviod name clashes in child classes.
A version attribute that stores the current version of the class and shoulnd't be passed to child classes, who will have their own versions.

### `__name__`
Reserved for built-in methods. A method that is run whenever the object is printed, constructor called, etc...


```python

```
