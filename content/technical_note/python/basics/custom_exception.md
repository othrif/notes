---
title: "Custom exception"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Handling exception 
Built-in exceptions inherit from class `BaseException` or `Exception`


```python
# MODIFY the function to catch exceptions
def invert_at_index(x, ind):
    try:
        return 1/x[ind]
    except ZeroDivisionError:
        print("Cannot divide by zero!")
    except IndexError:
        print("Index out of range!")
 
a = [5,6,0,7]

# Works okay
print(invert_at_index(a, 1))

# Potential ZeroDivisionError
print(invert_at_index(a, 2))

# Potential IndexError
print(invert_at_index(a, 5))
```

    0.16666666666666666
    Cannot divide by zero!
    None
    Index out of range!
    None


### Custom exception
Need to define an exception is a class inherited from the built-in `Exception` class or one of its subclasses.


```python
class SalaryError(ValueError): pass
class BonusError(SalaryError): pass

class Employee:
  MIN_SALARY = 30000
  MAX_BONUS = 5000

  def __init__(self, name, salary = 30000):
    self.name = name    
    if salary < Employee.MIN_SALARY:
      raise SalaryError("Salary is too low!")      
    self.salary = salary
    
  # Rewrite using exceptions  
  def give_bonus(self, amount):
    if amount > Employee.MAX_BONUS:
        raise BonusError("The bonus amount is too high!")  
        
    elif self.salary + amount <  Employee.MIN_SALARY:
        raise SalaryError("The salary after bonus is too low!")
      
    else:  
      self.salary += amount
```


```python
e = Employee('othmane',1000)
```


    ---------------------------------------------------------------------------

    SalaryError                               Traceback (most recent call last)

    <ipython-input-16-96ecb849cf7a> in <module>
    ----> 1 e = Employee('othmane',1000)
    

    <ipython-input-14-1dd77ad984a7> in __init__(self, name, salary)
          9     self.name = name
         10     if salary < Employee.MIN_SALARY:
    ---> 11       raise SalaryError("Salary is too low!")
         12     self.salary = salary
         13 


    SalaryError: Salary is too low!



```python
e = Employee('othmane',1000000)
```


```python
e.give_bonus(500000)
```


    ---------------------------------------------------------------------------

    BonusError                                Traceback (most recent call last)

    <ipython-input-18-0cfd0f4c6fd2> in <module>
    ----> 1 e.give_bonus(500000)
    

    <ipython-input-14-1dd77ad984a7> in give_bonus(self, amount)
         15   def give_bonus(self, amount):
         16     if amount > Employee.MAX_BONUS:
    ---> 17         raise BonusError("The bonus amount is too high!")
         18 
         19     elif self.salary + amount <  Employee.MIN_SALARY:


    BonusError: The bonus amount is too high!



```python
e.give_bonus(-980000)
```


    ---------------------------------------------------------------------------

    SalaryError                               Traceback (most recent call last)

    <ipython-input-20-c41bdf5a7cec> in <module>
    ----> 1 e.give_bonus(-980000)
    

    <ipython-input-14-1dd77ad984a7> in give_bonus(self, amount)
         18 
         19     elif self.salary + amount <  Employee.MIN_SALARY:
    ---> 20         raise SalaryError("The salary after bonus is too low!")
         21 
         22     else:


    SalaryError: The salary after bonus is too low!



```python

```
