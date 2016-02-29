
# Python Modules

* Any **py** file is **python module**
   * module can be imported as **python library**
   * module can be used as script (**python program**)
   * or both (using `__name__`)


## Creating and importing modules

* Create folder pyfund
* create file words.py
* content of the words.py is:      
```python
  def fetch_words():
      w = ["one", "two", "three"]
      print_words(w)

  def print_words(list):
      for item in list:
          print(item)
```
execute it in REPL:     
**import module**
```bash
cd pyfind
puthon3
>>> import words
>>> words.fetch_words()
one
two
three
```
**from module import function**
```bash
>>> from words import fetch_words
>>> fetch_words
one
two
three
```
__from module import *__
```bash
>>> from words import *
>>> fetch_words
one
two
three
```
**from module import (fetch_words, print_words)**

## Distinguish between Import and Execution

execute it in command prompt:
```bash
$python3 words.py    #nothing happens
```

**`__name__` evaluates to `__main__` or the actual module name depending on how the enclosing module is being used**

```python
  def fetch_words():
      w = ["one", "two", "three"]
      for item in w:
          print(item)
          
  print(__name__)   # add this to show usage of double undescore usage
```

execute it in REPL:
```bash
>>> import words
words               #when importing `__name__` is set to imported namespace only executed ONCE:
>>> import words
```
run in command:
```bash
$python3 words.py
__main__           #when running as a py program the `__name__` is set to `__main__`
```
We can use that to modify library:
```python
  def fetch_words():
      w = ["one", "two", "three"]
      for item in w:
          print(item)
          
  if __name__ == "__main__":
      fetch_words()
```
Now we can safely import this function AND also use it as a script

For command line arguments look at :
* argparse  (python standard library)
* docopt    (3rd party)
 
### Documenting code

```python
def some_function(arg1):
  """ what it does
  
  Args:
      arg1: description
      
  Returns:
      explain here
  """
```
it can be accessed with `help(some_function)`
For module place it at the very top

```python
#!/usr/bin/env python3
```
then you can run code as executable: `program.py` without: `python3 program.py`

#Python Objects

