
# VALUES
no variables but values (they cannot be changed at runtime (immutable)!)
```
let x = 100
x = 105 //does the comparison not even try assigning
```
 * u for uint
 * y for byte
 * L for int64
 * I for big int
 * m for decimal

# FUNCTIONS
are also values. 
Last expression is body is the return value!

```
let square x = x * x  //int is as default
```
```
let add x y =    //takes typle as parameters
  x + y
```
```
let add' x y = 
  let result =
    x + y
  result //return value
```
```
let add5and3 = add 5 3
```
```
let result= add (aquare 12) 7
```

