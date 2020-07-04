---
title: "Control attribute acess using @property"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### What are properties?

You could think of properties as attributes with built-in access control. They are especially useful when there is some additional code you'd like to execute when assigning values to attributes.
to a class user, they look just like regular attributes, but behind the scenes, they can have custom code executed when they are accessed.

### Create and set properties

There are two parts to defining a property:

- Define an "internal" attribute that will contain the data `_name`
- Define a `@property`-decorated method whose name is the property `name`, and that returns the internal attribute storing the data

If you'd also like to define a custom setter method, there's an additional step:

- Define another method whose name is exactly the property name (again), and decorate it with `@prop_name.setter` where `prop_name` is the name of the property. The method should take two arguments -- `self` (as always), and the value that's being assigned to the property.


```python
class Customer:
    def __init__(self, name, new_bal):
        self.name = name
        if new_bal < 0:
           raise ValueError("Invalid balance!")
        self._balance = new_bal  

    # Add a decorated balance() method returning _balance        
    @property
    def balance(self):
        return self._balance

    # Add a setter balance() method
    @balance.setter
    def balance(self, new_bal):
        # Validate the parameter value
        if new_bal < 0:
           raise ValueError("Invalid balance!")
        self._balance = new_bal
        print("Setter method called")

# Create a Customer        
cust = Customer('Belinda Lutz', 2000)

# Assign 3000 to the balance property
cust.balance = 3000

# Print the balance property
print(cust.balance)
```

    Setter method called
    3000


the user of your `Customer` class won't be able to assign arbitrary values to the customers' balance. 


```python

```
