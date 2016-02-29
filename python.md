
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

```python
phones = { ''vlad': '111-222-3336', 'ada': 222-555-6666}
phones['vlad']                    # '111-222-3336'
phones['vlad'] = '111-333-444'    # updates existing
phones['vladimir'] = '111-333-444'# create new one if not existing

e = {}              # Creates empty dictionary
```



