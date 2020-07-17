---
title: "Loading a pickled file"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Concept
if you merely want to be able to import them into Python, you can serialize them. All this means is converting the object into a sequence of bytes, or a bytestream.


```python
# Import pickle package
import pickle

# Open pickle file and load data: d
with open('data.pkl', 'rb') as file:
    d = pickle.load(file)

# Print d
print(d)

# Print datatype of d
print(type(d))
```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    <ipython-input-1-7b211b6854e7> in <module>
          3 
          4 # Open pickle file and load data: d
    ----> 5 with open('data.pkl', 'rb') as file:
          6     d = pickle.load(file)
          7 


    FileNotFoundError: [Errno 2] No such file or directory: 'data.pkl'

