---
title: "Error and exception"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Error handling with try-except


```python
def shout_echo(word1, echo=1):
    """Concatenate echo copies of word1 and three
    exclamation marks at the end of the string."""

    echo_word=''
    shout_words=''

    # Add exception handling with try-except
    try:
        echo_word = word1*echo
        shout_words = echo_word+'!!!'
    except:
        print("word1 must be a string and echo must be an integer.")
        
    return shout_words

shout_echo('particle', echo='accelerator')
```

    word1 must be a string and echo must be an integer.





    ''



### Error handling by raising an error


```python
def shout_echo(word1, echo=1):
    """Concatenate echo copies of word1 and three
    exclamation marks at the end of the string."""

    # Raise an error with raise
    if echo<0:
        raise ValueError('echo must be greater than or equal to 0')

    echo_word = word1*echo
    shout_words = echo_word+'!!!'

    return shout_word

shout_echo("particle", echo=-5)
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-13-85d647f11453> in <module>
         12     return shout_word
         13 
    ---> 14 shout_echo("particle", echo=-5)
    

    <ipython-input-13-85d647f11453> in shout_echo(word1, echo)
          5     # Raise an error with raise
          6     if echo<0:
    ----> 7         raise ValueError('echo must be greater than or equal to 0')
          8 
          9     echo_word = word1*echo


    ValueError: echo must be greater than or equal to 0

