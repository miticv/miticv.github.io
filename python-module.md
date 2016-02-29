
# Pythin Modules

##Creating and importing modules

* Create folder pyfund
* create file words.py
* content of the words.py is:      
```python
  def fetch_words():
      w = ["one", "two", "three"]
      for item in w:
          print(item)
```
execute it in REPL:
```bash
cd pyfind
puthon3
>>> import words
>>> words.fetch_words()
one
two
three
>>> from words import fetch_words
>>> fetch_words
one
two
three
```

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

