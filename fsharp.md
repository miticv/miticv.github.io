
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

#MODULES
like static class. 
First file is default runnable module. If have more files, you have to maintain order of files in your project!   
You can have multiple modules per file. But module cannot span across files.
```
module calc
let add x y = x + y
```
```
namespace calcs
module calc2 =   //must use = when multiple modules in the same file
  let add x y = x + y
  let square x = x * x
  
module calc3 =
   let mult x 7 = x * y
```

