The ContextProvider opens a IDatabaseContext for a Databaseconnection. IDatabaseContext containes methods that can be used to select, insert, update or delete data from a Database and to create or alter Database, Tables and Fields.
```csharp
// Sql Database
var provider = new SqlContextProvider(connectionString);
using (var context = provider.Open())
{
	// use context to create Queries
}

// Sqlite Database
var provider = new SqliteContextProvider(connectionString);
using (var context = provider.Open())
{
	// use context to create Queries
}
```