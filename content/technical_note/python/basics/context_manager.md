---
title: "Context manager: `with ... as ...`"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### `with ... as ...`
`as <variable name>` is not needed if a context manager does not return a value.


```python
# Open "alice.txt" and assign the file to "file"
with open('alice.txt') as file:
  text = file.read()

n = 0
for word in text.split():
    if word.lower() in ['cat', 'cats']:
        n += 1

print('Lewis Carroll uses the word "cat" {} times'.format(n))
```

    Lewis Carroll uses the word "cat" 4 times


### How to create a context manager
Syntax:
``` python
import contextlib
@contextlib.contextmanager
def my_context():
    # Add any set up code you need
    yield
    # Add any tear down code you need (optional)
```


```python

@contextlib.contextmanager
def my_context():
    print('start context')
    yield 9999
    print('good bye!')

```


```python
with my_context() as foo:
    print('foo is {}'.format(foo))
```

    start context
    foo is 9999
    good bye!


Write `timer()` context manager to figure out which of their functions is running too slow. Notice that the three elements of a context manager are all here: a function definition, a yield statement, and the @contextlib.contextmanager decorator. It's also worth noticing that timer() is a context manager that does not return an explicit value, so yield is written by itself without specifying anything to return.


```python
import time

@contextlib.contextmanager
def timer():
  """Time the execution of a context block.

  Yields:
    None
  """
  start = time.time()
  # Send control back to the context block
  yield
  end = time.time()
  print('Elapsed: {:.2f}s'.format(end - start))
```


```python
with timer():
  print('This should take approximately 0.25 seconds')
  time.sleep(0.25)
```

    This should take approximately 0.25 seconds
    Elapsed: 0.25s


### A read-only open() context manager
read-only version of the open() context manager to use in your project to not accidentally overwrite one of the files when trying to read it in.


```python
@contextlib.contextmanager
def open_read_only(filename):
  """Open a file in read-only mode.

  Args:
    filename (str): The location of the file to read

  Yields:
    file object
  """
  read_only_file = open(filename, mode='r')
  # Yield read_only_file so it can be assigned to my_file
  yield read_only_file
  # Close read_only_file
  read_only_file.close()

with open_read_only('alice.txt') as my_file:
  print(my_file.read())
```

    this is alice.txt counting how many CATS i have. yes i said cAts . Not just one cat , but many catS !


### Changing the working directory
change the current working directory back to what it was when they called in_dir(). This is important to do because your users might be relying on their working directory being what it was when they started the script. in_dir() is a great example of the CHANGE/RESET pattern that indicates you should use a context manager.


```python
def in_dir(directory):
  """Change current working directory to `directory`,
  allow the user to run some code, and change back.

  Args:
    directory (str): The path to a directory to work in.
  """
  current_dir = os.getcwd()
  os.chdir(directory)

  # Add code that lets you handle errors
  try:
    yield
  # Ensure the directory is reset,
  # whether there was an error or not
  finally:
    os.chdir(current_dir)
```

### Context manager patterns
Situation where using a context manager with exception handling `try-finally` that can be useful

Start   | Finish
---     | ---   
Open    | Close   
Lock    | Release   
Change  | Reset   
Enter   | Exit   
Start   | Stop  
Setup   | Teardown  
Connect | Disconnect  





```python

```
