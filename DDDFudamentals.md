
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


![NavigationMapEntities](https://github.com/miticv/miticv.github.io/raw/master/Images/DDDFudamentals/NavigationMapEntities.png)




