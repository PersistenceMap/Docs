## Add a Table to a Database
The following Sample adds two tables to the Database defined in the ConnectionString. 
The structure of the tables are defined with the object definition.  
| Table name | Defined by the Name of the Type                 |  
| Fields     | Defined and Named by the Properties of the Type |  
 
The Tables are only created when the Context is Commited.

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