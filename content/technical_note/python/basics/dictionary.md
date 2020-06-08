---
title: "Dictionaries"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Basics



```python
# Definition of dictionary
europe = {'spain':'madrid', 'france':'paris', 'germany':'berlin', 'norway':'oslo' }

# Print out the keys in europe
print(europe.keys())

# Print out value that belongs to key 'norway'
print(europe['norway'])
```

    dict_keys(['spain', 'france', 'germany', 'norway'])
    oslo


### Add/Remove an element


```python
europe['italy'] = 'rome'
```


```python
europe
```




    {'spain': 'madrid',
     'france': 'paris',
     'germany': 'berlin',
     'norway': 'oslo',
     'italy': 'rome'}




```python
del(europe['france'])
```


```python
europe
```




    {'spain': 'madrid', 'germany': 'berlin', 'norway': 'oslo', 'italy': 'rome'}




```python

```
