---
title: "Method belonging to a class object"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
# Working with Class and methods


```python
class Vehicle:
  def __init__(self,color):
    self.color=color
  def start(self):
    print("Starting engine")
  def showcolor(self):
    print(f"I am {self.color}")
```


```python
car=Vehicle('black')
```


```python
car.start()
```

    Starting engine



```python
car.showcolor()
```

    I am black



```python
class MyCounter:
    """Here is the doc string!"""
    def __init__(self, n=10):
        self.count = n
        
    def set_count(self,n):
        print()

me = MyCounter()
me.set_count(10)
print(me.count)
```

    10

