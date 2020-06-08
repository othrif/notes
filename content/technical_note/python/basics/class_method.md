---
title: "Method beloning to a class object"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
# Working with Class and methods


```python
class vehicle:
  def __init__(self,color):
    self.color=color
  def start(self):
    print("Starting engine")
  def showcolor(self):
    print(f"I am {self.color}")
```


```python
car=vehicle('black')
```


```python
car.start()
```

    Starting engine



```python
car.showcolor()
```

    I am black

