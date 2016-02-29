
# Python 3.3

from Netherland.     
Strongly type language.     
Dynamically typed (no check until runtime)     
Interpretive language     
Written in C     
Jutjon => Java     
IronPython => .NET     
Pypy => RPython     

Zen of Python     
Python 2.7 => 3.3         

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
loop and 4 spaces (do not use tabs):
```python
>>> for i in range(5):
...    x = i * 10  # 4 spaces for indentation
...    print(x)
...
0 
10
20
30
40
>>>
```
Arithmentic operators
* + 
* -
* *
* /
* %
* //


## [PEPS](https://www.python.org/dev/peps/): Zen of Python

[Peps 08](https://www.python.org/dev/peps/pep-0008/#tabs-or-spaces): 4 spaces no tabs
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

### Integers

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
### Float

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
### None
represent no value

```Python
>>> a = None
>>> a is None
True
```
### Bool

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
### Relational Operators

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
```
c=5
while c!= 0:
    print(c)
    c -= 1
```
Break while loop:
```
while True:
    if expr:
        break
```
## Strings and Collections
















