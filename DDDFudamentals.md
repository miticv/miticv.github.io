
# DDD Fudamentals

1 -- Interaction of Domain Experts (Spend time talking to domain experts)      
2 -- Model a single sub-domain at the time   
3 -- Implementation of Sub-Domain    

-- Not allways make sense to DDD (tick tac toe game example)   

![NavigationMap](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/NavigationMapLabeled.png)

-- we build the wrong ting or we build thing wrong :)     

Client in one context (Sched) means different thing than the Client in another context (Billling):    
![BondedContextClients](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/BondedContextClients.png)

They should be separated as if they are each their own micro service:    
Notification in Appointmet is totally different than Notification in Billing (notify different things)    
![ContextMapClients](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/ContextMapClients.png)

Both Sched and billing have *Shared Kernel* which is "User" in this case that they both use.
![ContextMapClientsStack](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/ContextMapClientsStack.png)

Glossary of language used to describe DDD   
Entity and Context used in DDD is very different than the one used in EF.   
![Glosary1](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/Glosary1.png)
![Glosary2](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/Glosary2.png)

## Anemic Domain Model vs Rich Domain Model
Focus on attributes vs behavioud

-- Anemic - focus on STATE of the Domain Models (and not behaviour)     
It has getter and setters, and nothing about behaviour. *They can be not bad if all you need is CRUD logic.*
It is *anti-pattern* for DDD since DDD is used when your model is too complex for simple CRUD.
Object, connected with rich relationships. But there are no behaviours just bags of getters and setters.
They come with rules NOT to put any domain logic in the domain objects. Instead - services using the object capture the domain logic.

-- Rich - focus on BEHAVIOUR of the Domain Models 

## Entitiy Objects

DDD is driven by behaviour, but we still need objects:   
Many objects are not fudamentally defined by their attribures - but by a thread of continuity and identity.   
There are 2 types of objects - defined by Identity and defined by Value   
The ones by Identity are called ENTITIES   

Entity has Key to identify it (has interface *IEntity* with id property: *int id;* IEntity<int>)      
Entity is easier to use GUID instead of ID (but not required!) (IEntity as string GUID; : IEntity<GUID>)          
![GUIDandINT](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/GUIDandINT.png)
-- this is interesting. If GUID it will be easier to "copy" data from PROD to lower environments also as opposed to hard binded-int tied to DB.

*Single Responsibility Principle of Entities*    
Entity doesn't have to have lots of busines logic in it.
If it does it is wrong, responsibility is keep very closed related responsibilities together.    
Design shouold focus on 2: ID and LIFE CYCLE     
Identity is ot just ID always - as when people are involved, proving who they are with SIN and Phone#. 
If too much then delegate verify identity to some other object to be responsible for that.       
Lifecycle of ups is rec, shipped, in transit, loc A, loc B, delivered. But if there is much more logic than hat then
use services that answer what is to be done with the package, or to value object with status logic.

*Also Entities should NOT have equality methods!!*     
(if you do ask yourself WHY are you asking that question?   
a) distributed DB with 2 same IDs      
b) duplicate customers inputed in system twice?    

--- Value entities *should* have equality methods.

*Consider not using bi-derictonal *
use One Way relationshiop instead.

![NavigationMapEntities](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/NavigationMapEntities.png)


## Value Objects

-- Measures, quantifies, or describes A THING in the domain    
-- Idenity is based on composition of the values of all properties   
-- Immutable (once created cannot change, you can create new one, dont set public setters.)    
-- Compared using all values   
-- No side effects (Any Methods or Behaviours only compute things, and does not change state of the object or the system)    
   (if new value is needed new value object is returned)   
   
   
Example **string** is value object. It    
Money is great Value Object: Point in time, Currency (US$) and Value (50k).      
DateRange is also Value Object: start, end.    

Use Value object instead of Entities whenever possible.    
### Start thinking as a Value Object, and if start having states - make it a Value Object
Value Object are great place to put method and logic - better place than Entities.

## Domain Services

Service operations should not belog to a particular Entity or Value Object    
(we dont want to shift our domain logic to services)
Should have defined interface   
Should be stateless
Service examples: 
-- UI Layer - Message Sending, Message Processing, XML Parsing, UI Services
-- Domain - Transfer between balnces, Process Order, ....
-- Infrastructure - Send Email, Log to a File

![Glosary3](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/Glosary3.png)
![Glosary4](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/Glosary4.png)

## Data Complexity

### Aggregates & Aggregate Roots

Relation One to Many (Root and Root's Invariant)   
ACID: Atomic, Consistent, Isolated, Durable   
Aggregate Root must maintain its invariants (Number and type of components in the example)   
When Deleating is cstading, then object in question is Aggregate Root.

Aggregate is a cluster of assiciated objects that we treat as a unit for the purpose of data changes.   
  
![AggregateRelationships](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/AggregateRelationships.png)
![Glosary5](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/Glosary5.png)


### Repositories

Think of it as in-mommory collection (doesnt care how it does it)   
Repositories for aggregate roots   
Client focus on model, repo focus on persistence    

Common issues:
1 - N+1 Query Errors: Fetch list and then fetch each item individually    
2 - Innapropriate use of eager or lazy loading   
3 - Fetching more data than required   


### Factories

Factories create new objects  (persistance NO NO NO)   
Repositores find and update existing objects (persistance YES YES YES)  
- repository can use Factory to create its objects.   

Implement IRepository<T>  (with List(), GetByd(), Insert(), Update(), Delete() )
if it is CRUD it makes sense (It is DDD recommendation for Aggregate Root), so you dont have to create separate one for each Entity.    
Catch is not to allow them to use this generic interface to access non-aggregate roots by adding IAggregateRoot
If it is not CRUD  - maybe might not make sense to implement all of it!!

![Generic](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/GenericOnlyForAggregateRoots.png)
![Glosary6](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/Glosary6.png)

### Domain Events




### Anti-Corryption Layers



