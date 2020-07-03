---
title: "Class-level attributes, alternative constructors, and inheritance of class methods"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Customize the constructor of the DataFrame
implement a small LoggedDF class that inherits from a regular pandas DataFrame but has a created_at attribute storing the timestamp. 


```python
# Import pandas as pd
import pandas as pd

# Define LoggedDF inherited from pd.DataFrame and add the constructor
class LoggedDF(pd.DataFrame):
  
  def __init__(self, *args, **kwargs):
    pd.DataFrame.__init__(self, *args, **kwargs)
    self.created_at = datetime.today()
    
    
ldf = LoggedDF({"col1": [1,2], "col2": [3,4]})
print(ldf.values)
print(ldf.created_at)
```

    [[1 3]
     [2 4]]
    2020-07-03 14:14:13.578281


### Customize a method of the DataFrame
Using `*args` and `**kwargs` allows you to not worry about keeping the signature of your customized method compatible. Notice how in the very last line, you called the parent method and passed an object to it that isn't self. When you call parent methods in the class, they should accept some object as the first argument, and that object is usually `self`, but it doesn't have to be!


```python
# Import pandas as pd
import pandas as pd

# Define LoggedDF inherited from pd.DataFrame and add the constructor
class LoggedDF(pd.DataFrame):
  
  def __init__(self, *args, **kwargs):
    pd.DataFrame.__init__(self, *args, **kwargs)
    self.created_at = datetime.today()
    
  def to_csv(self, *args, **kwargs):
    # Copy self to a temporary DataFrame
    temp = self.copy()
    
    # Create a new column filled with self.created at
    temp["created_at"] = self.created_at
    
    # Call pd.DataFrame.to_csv on temp with *args and **kwargs
    pd.DataFrame.to_csv(temp, *args, **kwargs)
    
```


```python
ldf = LoggedDF({"col1": [1,2], "col2": [3,4]})
print(ldf.values)
print(ldf.created_at)
```

    [[1 3]
     [2 4]]
    2020-07-03 14:14:14.769906

