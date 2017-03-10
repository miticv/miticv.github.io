
# Entity Framework Core

```
Install-package MicrosoftEntityFrameworkCore.SqlServer
```

Add classes SamuraiApp.Domain\
```
battle.cs  //if column name is named id - it will make it primary key in DB
quote.cs   // string is nvarchat(MAX), date is datetime2
samurai.cs
```
Add context  SamuraiApp.Data\
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
get-help EntityFrameworkCore
get-help Add-Migration
add-migration init  
```
init will create Migrations folder with init.cs file and contextModel snapshot
That way can track changes done on the database (in source controll also)

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




