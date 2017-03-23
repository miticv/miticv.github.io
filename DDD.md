# Domain Driven Design 

* Premature optimizatin is the root of all evil in software development - Donald Knuth
* The first concern of the architect is to make sure that the house is usable, it is not thatis made of brick - Uncle Bob

![Db vs Domain](https://github.com/miticv/miticv.github.io/raw/master/Images/DbVsDomain.png)

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
![Hexagonal](https://github.com/miticv/miticv.github.io/raw/master/Images/Hexagonal.png)
### Onion Architecture
![Onion](https://github.com/miticv/miticv.github.io/raw/master/Images/Onion.png)
### The Clean Architecture
![Clean](https://github.com/miticv/miticv.github.io/raw/master/Images/Clean.png)
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
![FourLayer](https://github.com/miticv/miticv.github.io/raw/master/Images/FourLayer.png)
* Implements use cases
* High level application logic
* Knows abot domain
* DOES'T know about infrastructure, persistance and presentation
* Contain interfaces
* Uses IoC (orange dependencies)
- Inverted Dependency (persistance and infrastructure depends on application)
Abstraction should not depend on detail, rather detail should depend on abstraction
- Independent deployability
- flexible and maintainable
- Dashed arrow is for ORM as optional
Can have contructor containing interfaces injected at the time of creation.


## Commands and Queries
CQRS is domain centric. One read and other write to database.
More efficient from coding perspective
Cons:
inconsistency in read/write, more complex


* Single database CQRS
Queries read using SP, scripts, LINQ, 
Commands write using EF, or other ORM.
![SingleCQRS](https://github.com/miticv/miticv.github.io/raw/master/Images/SingleCQRS.png)

* Two database SQRS
Read and write DBses
Write to NoSql, read from first normal form dbs. (read optimized) it is fast reading
![TwoDbCQRS](https://github.com/miticv/miticv.github.io/raw/master/Images/TwoDbCQRS.png)

* Event Sourcing CQRS
Store events
Replay events
Modify entity
Store new event
Update read database
![EvenSourcingCQRS](https://github.com/miticv/miticv.github.io/raw/master/Images/EvenSourcingCQRS.png)

