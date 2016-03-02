
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

# Python Objects

## Immutable
All python objects are IMMUTABLE other than lists(arrays and dictionaries)
```python
x = 100
x = 500  # creates new value and changes x pointer to new value
y = x    # y is pointing to the same 500 value
x = 600  # X points to 600 now, and y is still pointing to 500 !!!!

id(x) == id(y)    # would be False
x is y            # can also test it this way!
```

## pass by refference
When calling function - arguments are ALWAYS passed as REFFERENCES
```python
f = [1,2,3]
def replace(g):
    g = [5,6,7]    # f is unchanged! g is pointing to different list now.

def replace(g):
   g[0] = 5
   g[1] = 6
   g[2] = 7        # now f is changed :) 
```

## pass default value

Always must be specified after regular ones
```python
def banner(message, border='-'):
    line = border * len(message)
    print(line)
    print(message)
    print(line)

banner("test message")
banner("test message", "*")
banner(border="*", message="test message")   # here order doesnt matter
```

default arguments are ALWAYS executed only once!
**issue1**
```python
import time

def show(arg=time.ctime()):  #default argument with current date time.
    print(arg)

show()
show()         #show same time as 1st time
show()         #show same time as 1st time
```
proper fix for default values should be:
```python
def show(arg=None):  #default argument with current date time.
    if arg is None:
        arg=time.ctime()
    print(arg)
```

**issue2 with lists**
```python
def add_spam(menu=[]):  #default argument with empty list (created only once!)
    menu.append("spam")
    return menu
breakfast = ['bacon','eggs']
add_spam(breakfast)       #all as expected

add_spam()                # this gives ['spam'] as expected 
add_spam()                # this gives ['spam','spam'] since 
add_spam()                # this gives ['spam','spam','spam']
...
```
proper fix whould be:
```python
def add_spam(menu=None):  #use immutable object as argument
    if menu is None:      #and test if it is passed
        menu=[]
    menu.append("spam")
    return menu
```

## scope

**issue1**
```python
count = 0

def show_count():
    print("count = ", count)

def set_count(c):
    count = c            #this count is NEW LOCAL variable (not global one)
```
fix:
```python
count = 0

def show_count():
    print("count = ", count)

def set_count(c):
    global count         #this tells us that to use existing (not create new local count)
    count = c            
```


# Classes
By convention class names use CamelCase

create "airtravel.py":
```python
class Flight:
    pass

from airtravel import Flight
f = Flight()
type(f)
```
with single function
```python
class Flight:
    def number(self):
        return "SN060"

from airtravel import Flight
f = Flight()
f.number()            # "SN060"
Flight.number(f)      # same thing but very rarely used
```
with initialization:
```python
class Flight:
    def __init__(self, number):   # configures an object Flight that already exist when this is called (as opposed to constructor)
        self._number = number     # _ as a private 

    def number(self):
        return self._number

from airtravel import Flight
f = Flight("SN060")
f.number()            # "SN060"
```
Initializers:
Private protected and public: in Pythin EVERYTHING is public!
underscore does not hide implementation variable, it is consent
useful when debuging

Class Invariants
```python
class Flight:
    def __init__(self, number, aircraft):   
        if not number[:2].isalpha():
            raise ValueError("No Airline code in '{}'".format(number))
        if not number[:2].isupper():
            raise ValueError("Invalid Airline code in '{}'".format(number))
        if not number[2:].isdigit() and int(number[:2] <= 9999):
            raise ValueError("Invalid route number '{}'".format(number))
        
        self._number = number   
        self._aircraft = aircraft

    def number(self):
        return self._number

    def airline(self):
        return self._number[:2]
    
    def aircraft_model(self):
        return self._aircraft.model()   # calls model from subclass
                                        # Complex is better than complicated
    
from airtravel import Flight
f = Flight("SN060")
f.number()            # "SN060"
```
Functions are sometime appropriate without classes
"tell () dont ask (what is the state)"

Polymprphism - object fitness determined at the time of use
James Whitcomb Riley:
"When i see a bird that walks like a duck and swims like a duck and quacks like a duck, I call that bird a duck."

Python uses polimorhism by default. And it will succeed if fits on runtime

Inheritance
exclude duplicate code into base class

sample abstract class:
It would error out if you call num_seats():
```python
class Aircraft:
    
   def num_seats(self):
       rows, row_seats = self.seating_plan()   ## this class does not have seating_plan() therefore is ABSTRACT
       return len(rows) * len(row_seats)
       
       
class AirbusA319(Aircraft):      # this is how we  declare base class!
    ....
     
class Boing777(Aircraft):      # this is how we  declare base class!
    ....
```

# Files and Resource Management

open() to open file:
* file: filename
* mode: read/write/append, binary/text
* encoding: what kind - better explicit (different system might use different)

```python
f = open('somefile.txt', mode='wt', encoding='utf-8')
f.write(...)
f.close()

f = open('somefile.txt', mode='rt', encoding='utf-8')
f.read(32)      # number of characters (or bytes if byte file)
f.read()        # read remaining file
f.seek(0)       # go to begening
f.readline()    # read line, if at the end would return empty string
f.readlines()   # read lines in the array of strings
f.close()

f = open('somefile.txt', mode='at', encoding='utf-8')   #append
f.writelines(["line1\n", "line2"])                      # should add \n to each to match readlines() but dont have to
f.close()
```

```python
import sys

def main(filename):
   f = open('somefile.txt', mode='rt', encoding='utf-8')
   for line in f:
       sys.stdout.write(line)     # instead of print() which adds extra new line
   f.close()
   
```
use try finally to always close file!!
with-block
```python
with open('somefile.txt', mode='rt', encoding='utf-8') as f:
     return [ int(line.strip())] for line in f]
# now there is no need to manually close the file :) 
```

## binary files

```python
with open(flename, 'wb')  as bmp:
  bmp.write(b'BM')
  pixel_bookmark = bmp.tell()                 #
  bmp.write(b'\x00\x28')
  bmp.write(bytes((c,c,c,0)))                 # Blue Green Red Zero
  eof_bookmark = bmp.tell()
  
  bmp.seek(pixel_bookmark)
  bmp.write(_int32_to_bytes(eof_bookmark))
  
def _int32_to_bytes(i)
    return bytes(( i & oxff, 
                   i >> 8 & 0xff,
                   i >> 16 & 0xff,
                   i >> 24 & 0xff))
```

file-like objects
```python
def words_per_line(flo):
    return [len(line.split()) for line in flo.readlines()]

from urllib.request import urlopen
with urlopen('') as web_file:
    wp = words_per_line(web_file)

with open('somefile.txt', mode='rt', encoding='utf-8') as real_file:
    wp = words_per_line(real_file)
```

Create objects that can use with-block:

```python
from contextlib import closing

class Fridge:
    def open(self):
    
    def take(self, food):
    
    def close(self):
    
#now can use following:
with closing(Fridge()) as r:
    r.open()
    r.take(food)    # which will close door even if take raise exception!
```

# Unit Test

unittest
TestCase
fixtures
assertions

```python
import unittest

def analyze_text(filename):
     with open(filename, 'r') as f:
         return(sum(1 for _ in f)

class TextAnalysisTests(unittest.TestCase):

    def setUp(self):
        self.filename = 'testfile.txt'
        with open(self.filename, 'w') as f:
            f.write('some test line\n'
                    'another line\n' )
    def tearDown(self):
        try:
            os.remove(self.filename)
        except:
            pass
        
    def test_function_runs(self):
        analyze_text(self.filename)                       # basic smoke test: does the function run?

    def test_line_count(self):
        self.assertEqual(analyze_text(self.filename), 2)  # make sure line count equal is correct

    def test_no_such_file(self):
        with self.assertRaises(IOError):                  # make sure that IOError raises
            analyze_text('foobar')

if __name == '__main__':
    unittest.main()                                       # will run all the test cases if run file.py
```

PDB is command line tool debugger (like GBD)

```python
import pdb
pdb.set_trace()

# c continue
```
```
run code with `$ python3 -m pdb program.py` 
where     # call stack
next
next
print x   # can print expression or variables
cont      # let it run
^C        # stop program - return control to debugger
list      # to show source code of that line where we stopped
return    # return from current function
quit      # exit debugger
```
to enter break point go to that point and type `import pdb; pdn.set_trace()`
