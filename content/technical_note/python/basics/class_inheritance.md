---
title: "Class inheritance"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Class level attributes store data that is shared among all the class instances. They are assigned values in the class body and are refered to using the `ClassName` rather than `self` syntax  

### Class-level data
use `ClassName.ATTR_NAME` to accessthe class attribute value


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
        
# MODIFY Manager class and add a display method
class Manager(Employee):
  def display(self):
      print("Manager "+self.name)

mng = Manager("Debbie Lashko", 86500)
print(mng.name)

# Call mng.display()
mng.display()
```

    Debbie Lashko
    Manager Debbie Lashko




