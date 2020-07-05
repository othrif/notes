---
title: "Attaching nonlocal variables to nested functions"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Nested function
A function dened inside another function.


```python
# outer function
def parent():
    # nested function
    def child():
        pass
    return child
```

### Nonlocal variables
Variables dened in the parent function that are used by the child function


```python
def parent(arg_1, arg_2):
    # From child()'s point of view,
    # `value` and `my_dict` are nonlocal variables,
    # as are `arg_1` and `arg_2`.
    value = 22
    my_dict = {'chocolate': 'yummy'}
    def child():
        print(2 * value)
        print(my_dict['chocolate'])
        print(arg_1 + arg_2)
    return child
```


```python
my_func = parent([1], [2,3,4])
print(my_func)
my_func()
```

    <function parent.<locals>.child at 0x10c0cb048>
    44
    yummy
    [1, 2, 3, 4]


### Closure
Nonlocal variables attached to a returned function


```python
new_function = parent(3, 4)
print([cell.cell_contents for cell in new_function.__closure__])
```

    [3, 4, {'chocolate': 'yummy'}, 22]


### Checking for closure
Values passed to `return_a_func()` are still accessible to the new function returned, even after the program has left the scope of `return_a_func()`.

Values get added to a function's closure in the order they are defined in the enclosing function (in this case, `arg1` and then `arg2`), but only if they are used in the nested function. That is, if `return_a_func()` took a third argument (e.g., `arg3`) that wasn't used by `new_func()`, then it would not be captured in `new_func()`'s closure.


```python
def return_a_func(arg1, arg2, arg3):
  def new_func():
    print('arg1 was {}'.format(arg1))
    print('arg2 was {}'.format(arg2))
  return new_func
    
my_func = return_a_func(2, 17, 'hello')

print(my_func.__closure__ is not None)
print(len(my_func.__closure__))

# Get the values of the variables in the closure
closure_values = [
  my_func.__closure__[i].cell_contents for i in range(2)
]
print(closure_values)
```

    True
    2
    [2, 17]


### Closure keep your values safe
no matter what you do to `my_special_function()` after passing it to `get_new_func()`, the new function still mimics the behavior of the original `my_special_function()` because it is in the new function's closure.
even if you delete `my_special_function()`, you can still call `new_func()` without any problems.


```python
def my_special_function():
  print('You are running my_special_function()')
  
def get_new_func(func):
  def call_func():
    func()
  return call_func

new_func = get_new_func(my_special_function)

# Delete my_special_function()
del(my_special_function)

new_func()
```

    You are running my_special_function()


### Be aware!!!
you could run into memory issues if you wound up adding a very large array or object to the closure, and has resolved to keep her eye out for that sort of problem.


```python

```
