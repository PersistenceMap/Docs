## Stored Procedures
The Stored Procedure feature is only available on the SqlDatabaseContext.

### Stored Procedure without result
```csharp
context.Procedure("UpdateSalesByYear")
    .AddParameter("DateFrom", () => new DateTime(1970, 1, 1))
    .AddParameter(() => DateTime.Today)
	.AddParameter("@value", () => somevalue)
    .Execute();
```
### Stored Procedure with result
```csharp
var sales = context.Procedure("SalesByYear")
    .AddParameter(() => new DateTime(1970, 1, 1))
    .AddParameter(() => DateTime.Today)
    .Execute<SalesByYear>();
```
Map fields if the field names of the resultset and the data object don't match:
```csharp
var sales = context.Procedure("SalesByYear")
    .AddParameter(() => new DateTime(1970, 1, 1))
    .AddParameter(() => DateTime.Today)
    .For<SalesByYear>()
	.Map("OrdersID", sby => sby.ID)
	.Execute();
```
Convert a value from the resultset to a value in the data object:
```csharp
var sales = context.Procedure("SalesByYear")
    .AddParameter(() => new DateTime(1970, 1, 1))
    .AddParameter(() => DateTime.Today)
    .For<SalesByYear>()
	// converts the datetime provided by the result to a string
	.Map("Date", sby => sby.StringDate, value => ((DateTime)value).ToShortDateString())
	.Execute();
```
### Stored Procedure with output parameter
```csharp
int id = 0;
var proc = context.Procedure("SetSale")
    // adds a output parameter and executes the delegate after the procedure was executed
	.AddParameter("ID", () => id, ret => id = ret)
    .AddParameter("value", () => somevalue)
    .Execute<SalesByYear>();
```
