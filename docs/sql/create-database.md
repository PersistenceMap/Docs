PersistenceMap supports a code first approach. Databases, tables and fields can be created, altered or deleted at runtime.

## Create a Database
The following commands create a Database and two tables. The name of the Database is defined in the Connectionstring. The structure of the tables are defined with the object types.
The Database is only created when the Context is Commited.
```csharp
var provider = new SqlContextProvider(ConnectionString);
using (var context = provider.Open())
{
	// create the database
    context.Database.Create();
	
    context.Commit();
}
```