# Domain Design 

* Premature optimizatin is the root of all evil in software development - Donald Knuth
* The first concern of the architect is to make sure that the house is usable, it is not thatis made of brick - Uncle Bob

- Domain model is essential
- Use case is essential
- Presentation and persistance is not essesntial it is detail

Pros
Focus on Domain
Less coupling
Allows DDD

Cons
Requires more thought
Higher initial cost


### Hexagonal Architecture
![alt tag](https://raw.githubusercontent.com/miticv/miticv.github.io/master/images/Hexagonal.png)
### Onion Architecture

### The Clean Architecture

### Each has layers
in order to manage units of complexity:
- Level or abstraction
- Single Responsibility
- Isolate Roles and skills
- Multiple implementations
- Varying rates of change

## Domain Layer
has folders for each identity with IEntity
* Domain project contains our domain model which is an abstract representation of the business problem being solved.
* All of our classes, properties, methods should corespond to the concepts that exist in the bisiness world in the language of the business.
* There should be no abtraction leakage - there should not be any classes attributes or aspects in our domain model 
that pertain to the implementation details of the application. (like persistance, infrastructure or presentation)

## Application Layer
