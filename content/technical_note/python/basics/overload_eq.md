---
title: "Overload comparison operators"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Overloading equality
When comparing two objects of a custom class using `==`, Python by default compares just the object references, not the data contained in the objects. To override this behavior, the class can implement the special `__eq__()` method, which accepts two arguments -- the objects to be compared -- and returns True or False. This method will be implicitly called when two objects are compared.


```python
class BankAccount:
    def __init__(self, number, balance=0):
        self.balance = balance
        self.number = number
      
    def withdraw(self, amount):
        self.balance -= amount 
    
    # Define __eq__ that returns True if the number attributes are equal 
    def __eq__ (self, other):
        if type(self) == type(other):
            return (self.number == other.number)
        else:
            return False

# Create accounts and compare them       
acct1 = BankAccount(123, 1000)
acct2 = BankAccount(123, 1000)
acct3 = BankAccount(456, 1000)
print(acct1 == acct2)
print(acct1 == acct3)
    
```

    True
    False

