
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
## Entities 
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
c) 

--- Value entities should have equality methods.


![NavigationMapEntities](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/NavigationMapEntities.png)








