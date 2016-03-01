
# Python 3.3

* from Netherland.     
* Strongly type language.     
* Dynamically typed (no check until runtime)     
* Interpretive language     
* Written in C     

Other flavours:
* Jutjon => Java     
* IronPython => .NET     
* Pypy => RPython     

## Installation
* python.org, download page.
* WINDOWS download MSI and run
* C:\Python33\
* Add to path: C:\Python33; C:\Python33\Scripts

## Read Eval Print Loop (REPL)

_ operator
```python
>>> x = 5
>>> x
5
>>> _ * 2  # _ is for last value used (in our case 5)
10
Ctrl+Z to exit
```
Arithmentic operators
* + 
* -
* *
* /
* %
* //


## [PEPS](https://www.python.org/dev/peps/): Zen of Python

* Beautiful is better than ugly.
* Explicit is better than implicit.
* Simple is better than complex.
* Complex is better than complicated.
* Flat is better than nested.
* Sparse is better than dense.
   * 2 empty lines between functions [Peps 08](https://www.python.org/dev/peps/pep-0008/#tabs-or-spaces)
   
* Readability counts.
   * 4 spaces for indentation (not tabs) [Peps 08](https://www.python.org/dev/peps/pep-0008/#tabs-or-spaces)
   
* Special cases aren't special enough to break the rules.
   * all variables are references to objects
   * Everything in Python is object
* Although practicality beats purity.
   * avoid escape sequences and use 2 styles of quites " and '
   
* Errors should never pass silently.
   
* Unless explicitly silenced.
* In the face of ambiguity, refuse the temptation to guess.
* There should be one-- and preferably only one --obvious way to do it.
* Although that way may not be obvious at first unless you're Dutch.
* Now is better than never.
* Although never is often better than *right* now.
* If the implementation is hard to explain, it's a bad idea.
* If the implementation is easy to explain, it may be a good idea.
* Namespaces are one honking great idea -- let's do more of those!


 
[Peps 20](https://www.python.org/dev/peps/pep-0020/): Zen of Python or print it with `>>> import this`     

## Importing libraries

importing and help on command line
```python
>>>import math
>>>math.sqrt(81)
9.0
>>> help(math)
.. (q to exit)
>>> help(math.factorial)
...
```
importing different ways: 
```python
>>> import math                       #name colision possible with other libraries
>>> from math import factorial        #importing subset only
>>> from math import factorial as fac #import subset, and prevent name collisions
```

## Scalar types
* Immutable (Scalar Types) 
    * Integers 
    * Float
    * None
    * Bool
* Immutable (String and collections)
    * typles
    * Strings
    * Range
    * Bytes
* Mutable (Lists)
    * arrays
    * dictionaries

All objects in Python are immutable.
That means is always by reference, never copy object by value.

Immutable:
```python
x = 100
x = 500  # creates new value and changes x pointer to new value
y = x    # y is pointing to the same 500 value
x = 600  # X points to 600 now, and y is still pointing to 500 !!!!

id(x) == id(y)    # would be False
x is y            # can also test it this way!
```

### Integers (Immutable)
```python
>>> 10      #decimal
10
>>> 0b10    #binary
2
>>> 0o10    #octal
8
>>> 0x10    #hexi
16
>>int(3.5)
3
>>> int("496")
496
>>> int ("10000", 3)  #convert string to base 3 number
81
```
### Float (Immutable)

```python
>>> 3.125
3.125
>>> 3e8          # 3 * 10^8
300000000.0      
>>>1.616e-35     # 1.616 * 10^-35
1.616e-35
>>> float("1.234")
1.234
>>> float("nan")
nan
>>> float("inf")
inf
>>> float("-inf")
-inf
```
### None (Immutable)
represent no value

```python
>>> a = None
>>> a is None
True
```
### Bool (Immutable)

```python
>>>bool(0)       # 0 is False
False
>>>bool(0.0)     # 0.0 is False
False
>>>bool([])      # Empty collection is False
False
>>> bool("")     # Empty string is False
>>False
>>> bool(42)     # Anything else is True
True
```
#### Relational Operators

* ==   Equal
* !=   Not Equal
* <    less than
* >    greater
* <=   less or equal 
* >=   greater than or equal
 
### Conditional Statements

If statements:
* if True:
* if True:    
  else:
* if True:    
  elif:

While loop:
```python
c=5
while c!= 0:
    print(c)
    c -= 1
```
Break while loop:
```python
while True:
    if expr:
        break
```

```python
for intem in SomeList

for intem in SomeDictionary

```

## Strings and Collections (immutable)
immutable (cannot be changed)

### Tuple (immutable)
Heterogeneous immutable
```python
t = ()          # empty tuple
t = ("Vlad", 1973, 13.5)
t[0]             # "Vlad"
len(t)           # 3
for item in t:
    print(item)
t + ("Ada")       # can add to tuple (return new one with added item)
t * 3             # can multiply it (new one)

t = (5)
type(t)           # will be int !!!
t = (5,)
type(t)           # will be tuple
```
nested
```python
t = ((1,2), (2,3))
t[0][1]              # 2
```
can ommit paranthesis
```python
p = 1,2,3,4,5,6
```
usefull for returning multi part result of the function:
```python
def minmax(list):
    return min(list), max(list)
lower, upper = minmax([1,2,3,4,5,6,7,8])
```
arbitrary :
```python
(a,(b,(c,d))) = (4,(3,(2,1))
```
constructors"
```python
tuple([1,2,3,4])        # (1,2,3,4)
tuple("hello")          # ("h","e","l","l", "o")
```
containment
```python
5 in (1,2,3,4,5,6)     #True
5 not in (1,2,3,4,5,6) #False
```

### Strings (Immutable)
Homogeneous immutable of unicode characters

```python
len("hey")     # 3
```
Multiline strings
```python
""" this is
a multi line
string"""
'''so this is
also'''
```
escape sequences
```python
"this one contains ' "
'And this one contains " '
'this one contains \' and \" '
```
what you see is what you get: start with: `r`
```python
path = r'C:\some\path\no\need\for\excape\characters\here'
```
Pythin has no characters - only strings:
```python
s = 'test 123'
c = s[5]        #this is "1" as a one element string not character
s.capitalize()  # this is "Test 123" - it is returned as a new string!
```
joining
```python
"New" + "found" + "land"         #expensive
"".join(["New","found","land"])  #join then with empty separator string
colors = ';'.join(['white', 'blue', 'black'])  #separator.join 'white;blue;black'

```
splitting
```python
colors.split(";")                                                # split them back to array
t = "unforgetable".partition("forget")                           # ('un', 'forget', 'able')  # split in 3 partitions
origin, _ , dest = "unforgetable".partition("-")                 # _ is used as dummy variable in Python!
```
format
```python
"The age of {0} is {1}".format('Jim', 32)    # or:
"The age of {name} is {age}".format(name='Jim', age=32)

pos = (1,2,3)
"Position is x={pos[0]}, y={pos[1]}, z={pos[2]}".format(pos=pos)

import math
"pi={m.pi:.3f} and e={m.e.3f}".format(m=math)    # with 3 dec places
```

### Range
progression of integers

```python
range(5)           # 0,1,2,3,4  (stop)

range(5,10)        # 5,6,7,8,9  (start, stop)
list(range(3))     # [0,1,2]

range(0,10,2)      # 0,2,4,6,8  (start, stop, step)
```

enumerate
```python
t = [3, 13, 234, 6543]   # tuple
for p in enumerate(t):
   print(p)              
(0,3)
(1,13)
(2,234)
(3,6543)

for p in enumerate(t):                 # yealds (index, value)
   print("i={}, v={}".format(i,v))) 
```

### Bytes (Immutable)
Immutable 

```python
data = b'binary data now'
```
Unicode
```python
srpski = "дом"                    # unicode string
data = srpski.encode("utf-8")     #To Byte

serbian = data.decode("utf-8")    #To string
serbian = srpski                  #True
```

## List (mutable)

Heterogenious:
```python
numbs = [1,2,3,4]
strs = ["one", "two", "three"]
strs[2] = 2
  ["one", 2, "three"]                  # it is heterogenious!!!

s = "example of split string".split()  
s.count("of")                          # 1 => count instances of word "of"
s[0]                                   # "example"
s[-1]                                  # "string" negative is counting backwards

del s[1]           # same things. removes the element "of" from the list
s.remove("of")

s.insert(0, "An")  # insert the element at position 0

s = "example of split string".split(1:3)  # slice ["of","split","string"] .split(start,stop)
s[1:-1]                                   # slice all exept first and last ["of","split"]
s[2:] + s[:2]  == s                       # True

copy_string = s[:]    # Copies string (shallow copy)
copy_string is s      # False
copy_string == s      # True

copy_string = s.copy() # Copies string (shallow copy)
copy_string = list(s)  # Copies string (shallow copy)

g = [1,11,21,121,12321]
g.reverse()
g.sort()
g.sort(reverse=True)

y = sorted(x)
q = reversed(p)

```
shallow copy
```python
a = [[1,2],[3,4]]
b = a[:]
a is b    # False  
a == b    # True  


a[0] = [8,9]  # a is now [[8,9],[3,4]]             <= modified (new) element
              # while b is still [[1,2],[3,4]]     <= b is still pointing to old

a[1].append(5) # a  is now [[8,9],[3,4,5]]          <= appended 5
               # while b is still [[1,2],[3,4,5]]   <= also appended!


s = [[-1,1]] * 5
s[3].append(7)     # now ALL elements would have [-1,1,5] because * 5 did shallow copy.
```

append
```python
b = []
b.append(1.618)
b.append(3.14)
```
from list
```python
list("test")         #becomes: ["t","e","s","t"]
c = ['bear',
     'giraffe',
     'elephant', ]   #allowed , comma after the last element for maintainbility
```

## Dictionary (mutable)
key-value pair
Not sorted in any particular order
key is immutable while value can me mutable (changed)
we can add new values

```python
phones = { 'vlad': '111-222-3336', 'ada': 222-555-6666}
phones['vlad']                    # '111-222-3336'
phones['vlad'] = '111-333-444'    # updates existing
phones['vladimir'] = '111-333-444'# create new one if not existing

e = {}              # Creates empty dictionary

for key, value in phones.items():
    print("{key} => {value}".format(key=key, value=value))

del phones("vlad")

from pprint inport pprint as pp
pp(phones)
```

## Set (mutable)
Unorder collection of unique, immutable objects

```python
p = {1, 4, 6, 88}    # uses { same as dictionary, but without key:value format.
e = set()            #create empty set

s = set([2,23,5,2])  # will create set and remove duplicates
2 in s               # True
s.add(33)            # will add element 
s.add(2)             # will NOT add because 2 exists
s.update([2,4,323])  # add multiple elements

s.remove(2)          # has to be in the set - otherwise error
s.discard(2)         # doesnt not have to be memeber of the set.

j = s.copy()         # Shallow copy

#set operations
blue_eyes.union(blond_hair)          # blue eyes OR blond hair
blue_eyes.intersection(blond_hair)   # blue eyes AND blond hair
blue_eyes.difference(blond_hair)     # blue eyes AND NOT blond hair
blue_eyes.symmetric_difference(blond_hair)    # blue eyes OR blond hair but not both
blue_eyes.issubset(blond_hair)    # is blond hair subset of blue eyes
blue_eyes.issuperset(blond_hair)    # is blond hair superset of blue eyes
blue_eyes.isdisjoint(blond_hair)    # if 2 sets has none in common
```


Protocol | Collections | Test
------------ | -------------| -------------
 Container| str, list, range, tuple, bytes, set, dict        |  in and not in
 Sized    | str, list, range, tuple, bytes, set, dict        |  len(s)
 Iterable | str, list, range, tuple, bytes, set, dict        |  iter(s), for item in iterable:
 Sequence | str, list, range, tuple, bytes  |  item = seq[index], index = seq.index(item) num - seq.count(item), r = reversed(seq)
 Mutable Sequence | list  |   
 Mutable Set | set        |   
 Mutable Mapping | dict   |   
 
 
# Exceptions

```python
import sys

def convert(s):
    try:
        x = int(s)
    except ValueError:
        x = -1
    except TypeError:
        x = -1
    return x
```
same as:
```python
def convert(s):
    x = -1
    try:
        x = int(s)
    except (ValueError, TypeError):
        pass                            # pass is semantically empty code to fill the indentation 
    return x
```
or:
```python
def convert(s):
    try:
        return int(s)
    except (ValueError, TypeError) as e:
        print("Conversion error: {}"\
              .format(str(e)),
              file= sys.stderr)
        raise                            # raise error 
```
Do not catch `IdentationError`, `SyntaxError`, `NameError`. They are programmer errors.

* IndexError  when out of bound index is called
* ValueError object is right type, but innapropriate value
* KeyError when loop-up in a mapping fails
* TypeError - maybe do not use, but let program fail



2 phylosoplies:
* Look Before You Leap (LBYL)
  check all possible errors before you run. - bet you will miss something to check!
* Easier to Ask Forgiveness than Premission (EAFP) <= Python
  do not check anything. Handle error instead. 


```python
try:

except OSError as e:

    raise
finally:

```


# Iterables

##

[ expr(item) for item in iterable]
```python
words = "why sometimes I have belived as many as six impossible things before breakfast".split()

[len(word) for word in words]    # [3,9,1,4,8,2,4,2,3,10,6,6,9]

lengths = []                     #above line is the same as below:
for word in words:
    lengths.append(len(word))

```
[ expr(item) for item in iterable if predicate(item)]

## Iteration Protocols

```python
iterable = ['1','2','3','4']
iterator = iter(iterable)
next(iterator)
next(iterator)
next(iterator)
```

## Generators

```python
def gen123():
    yield 1
    yield 2
    yield 3    

g = gen123()
next(g)
next(g)
next(g)
```
good for infinite seq. 
lazy computing
```python
def take(count, iterable):
   copunter = 0
   for item in iterable:
       if counter == count:
           return
       counter += 1
       yield item

```
example of infinite:
```python
def lucas():
    yield 2
    a = 2
    b = 1
    while True:
        yield b
        a, b = b, a+b
  
for x in lucas():
    print(x)
```
To create generator from this:
[ expr(item) for item in iterable]
use brackets insead:!!
**(expr(item) for item in iterable )**

```python
million_squares = (X*X for x in range(1,1000001))
list(million_squares)   # looong list 
list(million_squares)   #  [] 


sum(X*X for x in range(1,1000001))    # very fast and efficient since it is not evaluating the list!
```

###intertools

any([False, False, True])     # True
all([False, False, True])     # False

zip
```python
sunday = [4,3,5]
monday = [1,2,3]

for item in zip(sunday, monday):   # can accept more than 2 iterables
    print(item)     # (4,1)
                    # (3,2)
                    # (5,3)
    
```
chain
```python
from intertools import chain
temps = chain(sunday, monday)

```
