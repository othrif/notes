---
title: "Docstrings: google style and numpydoc"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Google style


```python
def count_letter(content, letter):
  """Count the number of times `letter` appears in `content`.

  Args:
    content (str): The string to search.
    letter (str): The letter to search for.

  Returns:
    int

  # Add a section detailing what errors might be raised
  Raises:
    ValueError: If `letter` is not a one-character string.
  """
  if (not isinstance(letter, str)) or len(letter) != 1:
    raise ValueError('`letter` must be a single character string.')
  return len([char for char in content if char == letter])
```




### Numpydoc


```python
def function(arg_1, arg_2=42):
    """
    Description of what the function does.
    
    Parameters
    ----------
    arg_1 : expected type of arg_1
        Description of arg_1.
    arg_2 : int, optional
        Write optional when an argument has a default value.
        Default=42.
        
    Returns
    -------
    The type of the return value
        Can include a description of the return value.
        Replace "Returns" with "Yields" if this function is a generator
    """
    pass
```

### Retriving docstrings

#### `help()`


```python
help(count_letter)
```

    Help on function count_letter in module __main__:
    
    count_letter(content, letter)
        Count the number of times `letter` appears in `content`.
        
        Args:
          content (str): The string to search.
          letter (str): The letter to search for.
        
        Returns:
          int
        
        # Add a section detailing what errors might be raised
        Raises:
          ValueError: If `letter` is not a one-character string.
    


#### `__doc__`


```python
docstring = count_letter.__doc__

border = '#' * 100
print('{}\n{}\n{}'.format(border, docstring, border))
```

    ####################################################################################################
    Count the number of times `letter` appears in `content`.
    
      Args:
        content (str): The string to search.
        letter (str): The letter to search for.
    
      Returns:
        int
    
      # Add a section detailing what errors might be raised
      Raises:
        ValueError: If `letter` is not a one-character string.
      
    ####################################################################################################


#### Module `inspect.getdoc()`
Preferred way for visually pretty doc!


```python
import inspect

# Get the docstring with a function from the inspect module
docstring = inspect.getdoc(function)

border = '#' * 100
print('{}\n{}\n{}'.format(border, docstring, border))
```

    ####################################################################################################
    Description of what the function does.
    
    Parameters
    ----------
    arg_1 : expected type of arg_1
        Description of arg_1.
    arg_2 : int, optional
        Write optional when an argument has a default value.
        Default=42.
        
    Returns
    -------
    The type of the return value
        Can include a description of the return value.
        Replace "Returns" with "Yields" if this function is a generator
    ####################################################################################################


### Tools to generated docs:
There are some wonderful tools like `sphinx` and `pydoc` that will automatically generate online documentation for you based off of your docstrings.
