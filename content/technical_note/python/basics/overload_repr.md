---
title: "Overload comparison operators"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### String representation of objects
There are two special methods in Python that return a string representation of an object. `__str__()` is called when you use print() or str() on an object, and `__repr__()` is called when you use `repr()` on an object, print the object in the console without calling print(), or instead of `__str__()` if `__str__()` is not defined.

`__str__()` is supposed to provide a "user-friendly" output describing an object, and `__repr__()` should return the expression that, when evaluated, will return the same object, ensuring the reproducibility of your code.


```python
class Employee:
    def __init__(self, name, salary=30000):
        self.name, self.salary = name, salary
      
    def __str__(self):
        s = "Employee name: {name}\nEmployee salary: {salary}".format(name=self.name, salary=self.salary)      
        return s
      
    # Add the __repr__method  
    def __repr__(self):
        emp_repr = f'Employee("{self.name}",{self.salary})'
        return emp_repr
```

    Employee name: Amar Howard
    Employee salary: 30000
    Employee("Carolyn Ramirez",35000)



```python
emp1 = Employee("Amar Howard", 30000)
print(emp1)
```

    Employee name: Amar Howard
    Employee salary: 30000



```python
emp2 = Employee("Carolyn Ramirez", 35000)
print(repr(emp2))
```

    Employee("Carolyn Ramirez",35000)

