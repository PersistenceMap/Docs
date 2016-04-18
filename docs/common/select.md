
## Select
Simple select from a ***single*** Table:
```csharp
context.Select<Order>(o => o.ID == 1)
```
The Output will be mapped to **TODO: Edith this**

## Select with Join
Join ***multiple*** Tables together into one Dataobject:
```csharp
context.From<Order>()
	.Join<OrderDetail>((od, o) => od.OrderID == o.ID)
	.Select<OrderWithDetail>()
```
This will create the following Sql query:
**TODO: Edith this**
```sql
SELECT ProductID, OrderID from Order join OrderDetail on (OrderDetail.OrderID = Order.ID)
```
The Output will be mapped to **TODO: Edith this**

**TODO: Edith this**
Create a anonymous object that ***defines*** the fields for the select:
```csharp
context.From<Order>()
	.Join<OrderDetail>((od, o) => od.OrderID == o.ID)
	.For(() => new { ProductID = 0, OrderID = 0 })
	.Select(a => new OrderDetail { ProductID = a.ProductID, OrderID = a.OrderID })
```
Compiles to:
```sql
select ProductID, OrderID from Order join OrderDetail on (OrderDetail.OrderID = Order.ID)
```
The Output will be mapped to **TODO: Edith this**