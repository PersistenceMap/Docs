PersistenceMap supports a code first approach. Databases, tables and fields can be created, altered or deleted at runtime.

## Create a Database
The following commands create a Database and two tables. The name of the Database is defined in the Connectionstring. The structure of the tables are defined with the object types.

```csharp
var provider = new SqlContextProvider(ConnectionString);
using (var context = provider.Open())
{
	// create the database
    context.Database.Create();
	
    context.Commit();
}
```

## Add a Table to a Database
```csharp
var provider = new SqlContextProvider(ConnectionString);
using (var context = provider.Open())
{
	// create a table with a key
	context.Database.Table<Weapon>().Key(wpn => wpn.ID).Create();
	
	// table with a foreign key
	context.Database.Table<Warrior>().Key(wrir => wrir.ID).ForeignKey<Weapon>(wrir => wrir.WeaponID, wpn => wpn.ID).Create();
	
    context.Commit();
}
```