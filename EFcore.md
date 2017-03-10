
# Entity Framework Core
for .net core 1.1 (supports project.json)
`dotnet` shows you .net core version, and `dotnet --version` shows you version of SDK you installed

## Creating Models and create Databases

Extensions used:
Add New File
Open Command Line

```
Install-package MicrosoftEntityFrameworkCore.SqlServer
```

Add classes SamuraiApp.Domain\   Class Library(.NET Core)
```
battle.cs  //if column name is named id - it will make it primary key in DB
quote.cs   // string is nvarchat(MAX), date is datetime2
samurai.cs
```
Add context  SamuraiApp.Data\  Class Library(.NET Core) (add reference to domain in here also)
```
public class SamuraiContext : DbContext
  {
    public DbSet<Samurai> Samurais { get; set; }
    public DbSet<Battle> Battles { get; set; }
    public DbSet<Quote> Quotes { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
      optionsBuilder.UseSqlServer(
        "Server = (localdb)\\mssqllocaldb; Database = SamuraiData; Trusted_Connection = True; ");
    }
   }
```
Migration commands
```
Install-Package MicrosoftEntityFrameworkCore.Tools -pre

```
Open Command prompt inside SamuraiApp.Data:
```
dotnet
dotnet ef  //compiles but cannot invoke command on the startup project if it is not executable!!! (from class library)
```
create executable project Console Application (.NET Core)
Add references to SamuraiApp.Domain and SamuraiApp.Data
```
dotnet ef --startup-project ../CoreUI
```
has options for:
*database* - drop - update
*dbcontext*  -
*migrations* - add  - list - remove - script

```
dotnet ef --startup-project ../CoreUI migrations add init
```
(need to have `Microsoft.EntityFrameworkCore.Design` package to the CoreUI project!)

init will create Migrations folder with init.cs file and contextModel snapshot
That way can track changes done on the database (in source controll also)

```
dotnet ef --startup-project ../CoreUI database update
```

Script-Migration
```
Script-Migration
- scripts all migrations (default)

Script-Migration -Idempotent
- script all migrations - but do NOT apply changes that are there already

Script-Migration -From [migration] -To [migration]
which ranges are scripted
```

```
update-database -verbose
```

## Mapping and Migrations

### Many to Many
*:* (many to many) not supported in EF Core 1.1, only way is to create DomainClass that map both classes together
SamuraiBattle

```
public partial class SamuraiBattle
    {
        public int BattleId { get; set; }    //we will create join key
        public int SamuraiId { get; set; }

        public virtual Battle Battle { get; set; }
        public virtual Samurai Samurai { get; set; }
    }
```
add fluent API in the context class: (that way we are not express db schema in the domain classes)
```
protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<SamuraiBattle>(entity =>
            {            
                entity.HasKey(e => new { e.BattleId, e.SamuraiId })
                    .HasName("PK_SamuraiBattle");               
            });
```
use migration
```
add-migration JoinTable
```

### One to One

primary is foregin key
required is not nullable

Create new class "SecretIdentity"
```
    public partial class SecretIdentity
    {
        public int Id { get; set; }
        public string RealName { get; set; }
        public Samurai SamuraiId { get; set; }

        public int SamuraiId { get; set; }   <===========
    }
```
update Samurai class
```
public partial class Samurai
    {
        public Samurai()
        {
            Quotes = new List<Quote>();
        }

        public int Id { get; set; }
        public string Name { get; set; }

        public ICollection<Quote> Quotes { get; set; }
        public ICollection<SamuraiBattle> SamuraiBattle { get; set; }
        public SecretIdentity SecretIdentity { get; set; }     <===========
    }
```
and add requirements
```
model.Builder.Entity<Samurai>.Property(s=>s.SecretIdentity).IsRequired();
```
migrate it
```
add-migration SecretIdentity
```
It will clreate new migration object. It creates cascade delete on one to one relationship also!
now lets update the schema

####Snapshot
Every time you add the migration, it will update the snapshot
Snapshot is fluent way to describe the model, it is not migration code at all!
- If you make change and you were not happy - you can `remove migration` to remive last migration file and update snapshot accordingly
So do not just delete migration file, it will mess up the snapshopt, always use `remove migration` command instead
-If you updated the database, `remove migration` will not touch the database. you need to call `update database` command that will call drop method
- If you made change to the model, added a migration, `remove migration` will not fix the model - only snapshot and migration file

```
dotnet ef migrations remove --startup-project ../CoreUI
```

Migrations
```
script-migration  //creates scripts
script-migration -idempotent //also runs to all migrations, but check history table to know which update to run
script-migration -from JoinTable -to SecretIdentity  // from means from next one after JoinTable!!
script-migration -from init
update-database -verbose  // will create latest script in memmory and execute to the database
```

### scafolding
is creating model from existing database

```
dotnet ef dbcontext scaggold "conn string" provider --startup-project ../CoreUI
```

## Interacting with EF Core Model

EFCore uses: Mictosoft.Extensions.Logging.ILoggerProvider (that is generic for all loggers across core)

```
var samurai = new Samurai {Name = "Vlad"};
using (var context = new SamuraiContext()){
  context.GetService<ILoggerFactory>().AddProvider(new MyLoggerProvider());
  context.Samurais.Add(samurai);
  //context.Add(samurai); //or can add it like this
  context.SaveChanges();
}

//for logging you can add in OnConfiguring to show parameters during logging
optionsBuilder.EnableSensitiveDataLogging(); 

```

## Batch command saving
```
context.Samurais.AddRange(new List<Samurai> {samurai, samurai2 });
//we can change maxBatchSize - default is 100, so if more it will group them in batches of 100.
//to change:
protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
      optionsBuilder.UseSqlServer(
        "Server = (localdb)\\mssqllocaldb; Database = SamuraiData; Trusted_Connection = True; ", 
        options => options.MaxBatchSize(30));
    }
```

Get list of objects:
```
var samurais = context.Samurais.ToList();
var vlads = context.Samurais.Where(s=>s.Name == "Vlad").ToList();
var query = context.Samurais; //it will execute when enumerating it, or when calling toList() or other LINQ calls.
//be carefull of doing operations inside foreach - because that cause connection to be open!!!
//instead get results to list, then on list do foreach.
``

make one context in the class:
```
public static SamuraiContext _context = new SamuraiContext()

var samurai = _context.Samurais.Where(s=>s.Name == "Vlad").ToList();
```

First() Single() and Last() throw exception if no result
FirstOrDefault() <= will ALWAYS go to database to find result
Find()  <= will look in memmory and if not found then go to Database


### updates

```
//update
 var samurai = _context.Samurais.First();
  samurai.Name += " Mitic";
  _context.SaveChanges();
  
 //batch update (single sql command)
   var samurais = _context.Samurais.ToList();
   samurais.ForEach(s=>s.Name += ".");
  _context.SaveChanges();
  
  //batch update + insert (single sql command)
   var samurai = _context.Samurais.First();
  samurai.Name += " Mitic";
  _context.Samurais.Add(new Samurai { Name = "Ada"});
  _context.SaveChanges();
```

### Disconnected updates
websites or APIs - Design short-lived DbContext! (create them in controller for example, so it is new for each request)


### Deleting 
DbContext can only delete object it is aware of (already tracking)

```
_context.Samurais.Remove(samurai);  //find it and then delete it.
_context.SaveChanges();             //send only primary key value to delete it

//why there is no delete(int) like it is in Find(int)?
//it is coming
//can use stored proc to delete also
```

## call raw SQL

```
var samurais = _context.Samurais.FromSql("Select * from Samurais").ToList();
var samurais = _context.Samurais.FromSql("Select * from Samurais")
                .OrderByDescending(s => s.Name).ToList();                  //do sql sorting (not client side)
var samurais = _context.Samurais.FromSql("Select * from Samurais")
                .OrderByDescending(s => s.Name)
                .Where(s=>s.Name.Contais("ad")                             //do sql filtering (not client side)
                .ToList();
```

## call Stored Procedures

```
var namePart = "ad";
var samurais = _context.Samurais.FromSql("EXEC FilterSamuraiByNamePart {0}", namePart)
              .OrderByDescending(s => s.Name)    //// order by is now applied on the result in memmory not on sql server!
              .ToList();
```

ExecuteSqlCommand() - return int (rows affected). can use output parameters, does not run inside transaction
```

```

