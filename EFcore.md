


Install-package MicrosoftEntityFrameworkCore.SqlServer

Add classes
SamuraiApp.Domain\battle.cs
SamuraiApp.Domain\quote.cs
SamuraiApp.Domain\samurai.cs

SamuraiApp.Data\
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
