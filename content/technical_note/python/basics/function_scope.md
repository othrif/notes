---
title: "Modifying variables outside local scope: global, nonlocal"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### `global`
Sometimes your functions will need to modify a variable that is outside of the local scope of that function. While it's generally not best practice to do so, it's still good to know-how in case you need to do it. Update these functions so they can modify variables that would usually be outside of their scope.


```python
call_count = 0

def my_function():
  # Use a keyword that lets us update call_count 
  global call_count
  call_count += 1
  
  print("You've called my_function() {} times!".format(
    call_count
  ))
  
for _ in range(20):
  my_function()
```

    You've called my_function() 1 times!
    You've called my_function() 2 times!
    You've called my_function() 3 times!
    You've called my_function() 4 times!
    You've called my_function() 5 times!
    You've called my_function() 6 times!
    You've called my_function() 7 times!
    You've called my_function() 8 times!
    You've called my_function() 9 times!
    You've called my_function() 10 times!
    You've called my_function() 11 times!
    You've called my_function() 12 times!
    You've called my_function() 13 times!
    You've called my_function() 14 times!
    You've called my_function() 15 times!
    You've called my_function() 16 times!
    You've called my_function() 17 times!
    You've called my_function() 18 times!
    You've called my_function() 19 times!
    You've called my_function() 20 times!


### `nonlocal`


```python
def read_files():
  file_contents = None
  
  def save_contents(filename):
    # Add a keyword that lets us modify file_contents
    nonlocal file_contents
    if file_contents is None:
      file_contents = []
    with open(filename) as fin:
      file_contents.append(fin.read())
      
  for filename in ['1984.txt', 'MobyDick.txt', 'CatsEye.txt']:
    save_contents(filename)
    
  return file_contents
```
