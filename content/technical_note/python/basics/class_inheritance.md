---
title: "Class inheritance"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Class inheritance
Allows us to reuse and customize code without rewriting existing code. By calling methods of the parent class within the child class, we reuse all the code in those methods, making our code concise and manageable.

`Manager` employee "is-a" `Employee` = 'is-a' Relationship.
Example of customizing functionality via inheritance 


```python
class Employee:
  MIN_SALARY = 30000    

  def __init__(self, name, salary=MIN_SALARY):
      self.name = name
      if salary >= Employee.MIN_SALARY:
        self.salary = salary
      else:
        self.salary = Employee.MIN_SALARY
  def give_raise(self, amount):
    self.salary += amount      
        
# Manager class inherits from Employee class and add a display method
class Manager(Employee):
    def display(self):
      print("Manager "+self.name)

    def __init__(self, name, salary=50000, project=None):
        Employee.__init__(self, name, salary)
        self.project = project

    def give_raise(self,amount,bonus=1.05):
        Employee.give_raise(self, amount*bonus)

mng = Manager("Debbie Lashko", 86500)
print(mng.name)

# Call mng.display()
mng.display()

mngr = Manager("Ashta Dunbar", 78500)
mngr.give_raise(1000)
print(mngr.salary)
mngr.give_raise(2000)
print(mngr.salary)
```

    Debbie Lashko
    Manager Debbie Lashko
    79550.0
    81650.0


### Inheritance of class attributes


```python
class Boss(Employee):
    MIN_SALARY = 300000
 

e = Employee('employee')
b = Boss('boss')

print("e.MIN_SALARY = ", e.MIN_SALARY)
print("b.MIN_SALARY = ", b.MIN_SALARY)
```

    e.MIN_SALARY =  30000
    b.MIN_SALARY =  300000

