
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


