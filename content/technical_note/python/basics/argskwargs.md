---
title: "*args, **kwargs"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Functions with variable arguments (*args)
It allows you to pass a variable number of arguments to functions.


```python
def gibberish(*args):
    """Concatenate strings in *args together."""

    hodgepodge = ''

    for word in args:
        hodgepodge += word

    return hodgepodge

# Call gibberish() with one string: one_word
one_word = gibberish('luke')

# Call gibberish() with five strings: many_words
many_words = gibberish("luke", "leia", "han", "obi", "darth")

# Print one_word and many_words
print(one_word)
print(many_words)
```

    luke
    lukeleiahanobidarth


### Functions with variable-length keyword arguments (**kwargs)
It allows you to pass a variable number of keyword arguments to functions. Wthin the function definition, kwargs is a dictionary.


```python
def report_status(**kwargs):
    """Print out the status of a movie character."""

    print("\nBEGIN: REPORT\n")
    for key, val in kwargs.items():
        print(key + ": " + val)
    print("\nEND REPORT")
```


```python
report_status(name="luke", affiliation="jedi", status="missing")
```

    
    BEGIN: REPORT
    
    name: luke
    affiliation: jedi
    status: missing
    
    END REPORT



```python
report_status(name="anakin", affiliation="sith lord", status="deceased")
```

    
    BEGIN: REPORT
    
    name: anakin
    affiliation: sith lord
    status: deceased
    
    END REPORT



```python

```
