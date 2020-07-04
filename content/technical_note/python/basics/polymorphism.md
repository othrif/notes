---
title: "Polymorphysm methods"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Polymorphism and instances
Polymorphism ensures that the exact method called is determined dynamically based on the instance.


```python
class Parent:
    def talk(self):
        print("Parent talking!")     

class Child(Parent):
    def talk(self):
        print("Child talking!")


class TalkativeChild(Parent):
    def talk(self):
        print("TalkativeChild talking!")
        Parent.talk(self)


p, c, tc = Parent(), Child(), TalkativeChild()

for obj in (p, c, tc):
    obj.talk()
```

    Parent talking!
    Parent talking!
    TalkativeChild talking!
    Parent talking!


### Liskov Substitution Principal
the substitution principle requires the substitution to preserve the oversall state of the program.

#### Violations of LSP: Square-Rectangle problem 
it seems like you should be able to define a class Rectangle, with attributes h and w (for height and width), and then define a class Square that inherits from the Rectangle. After all, a square "is-a" rectangle!

Unfortunately, this intuition doesn't apply to object-oriented design.


```python
# Define a Rectangle class
class Rectangle:
    def __init__(self, h, w):
      self.h, self.w = h, w

# Define a Square class
class Square(Rectangle):
    def __init__(self, w):
      self.h, self.w = w, w  

```
