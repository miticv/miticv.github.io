
F# is hybrid supporting clases while being functional language also!

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
namespace calcs  //must use namespace when multiple modules in the same file
module calc2 =   //must use = when multiple modules in the same file
  let add x y = x + y
  let square x = x * x
  
module calc3 =   //must use = when multiple modules in the same file
   let mult x 7 = x * y
```

#CLASSES and ENUMS

enum type:
```
type CarType = 
   | Tricar = 0
   | StandardFourWHeeler = 1
   | HeavyLoadCarrier = 2
   | WierdContraption = 3
   | CrazyMonster = 4
```
```
type Car(color: string, wheelCount: int) =               //class declaration
   do                                                    //check parameters and raise exceptions
      if wheelCount < 3 then 
         failwith "how come?!"
      if wheelCount > 99 then
        failwioth "ridicilous"

   let carType = 
      match wheelCount with
      | 3 -> CarType.Tricar 
      | 4 -> CarType.StandardFourWHeeler
      | 6 -> CarType.HeavyLoadCarrier
      | x when x %2 = 1 -> CarType.WierdContraption
      | _ -> CarType.CrazyMonster
   new() = Car("red")                                                  //SECONDARY constructor without parameters!
   member x.Move() = printg "The %s car (%A) is moving" color carType  //x is SELF reference! You can use self instead also

let car = Car()
car.Move()

let gcar = Car("green")
gcar.Move()
```

#MUTABLE
create mutible properties as getter and setter

```
let mutable m = 10
m <- 20
```
getter and setter:
```
type Car
   let mutable passengerCount = 0
   
   member x.passengerCount with get() = passengerCount and set v = passengerCount <- v
   
let car = Car()
printfn "Car has %d passengers" car.passengerCount
car.passengerCount <- 2
printfn "Car has %d passengers" car.passengerCount
```
