#### Types of LINQ Syntax
- LINQ in .NET provides two main types of syntax for writing queries. Each has its own style, use cases, and practical implications.
**1. Query Syntax**
**2. Method Syntax**
   
1. **Query Syntax**:(Declarative Syntax)
- Query syntax resembles **SQL like statements**.
- It is declarative, describing what to retrieve rather than how to retrieve it.
- It is often preferred for simple, stand-alone queries that involve filtering, ordering, and projection.
- Query Syntax uses C# keywords like `from`, `where`, `select`, and `orderby` to define a query block.
- It is a declarative style, meaning it describes what data one wants, rather than how to get it.
```csharp
int[] numbers = { 1, 2, 3, 4, 5, 6 };

// Select even numbers using query syntax
var evenNumbers = from n in numbers
                  where n % 2 == 0
                  select n;

foreach(var num in evenNumbers)
{
    Console.WriteLine(num); // Output: 2, 4, 6
}
```
| **Aspect** | **Detail** |
|---|---|
| **Pro** | Highly readable and intuitive for multi-clause queries (especially complex joins or grouping). |
| **Con** | Less flexible; not all LINQ operators (e.g., `FirstOrDefault()`, `Count()`) are available as keywords and must be appended using Method Syntax. |

2. **Method Syntax**:(Fluent Syntax /Lambda Syntax)
- This syntax uses Extension Methods defined in `System.Linq`
- combined with `lambda expressions` applied directly to the data source (`IEnumerable<T>` or `IQueryable<T>`).
- Method Syntax, also known as Fluent Syntax, involves chaining standard query operator methods (`like` `.Where()`, `.Select()`, `.OrderBy()`) one after the other.
-  It is an object-oriented style that leverages the C# language features extensively. Preferred when using advanced LINQ features like Join or GroupBy.
```Csharp
int[] numbers = { 1, 2, 3, 4, 5, 6 };

// Select even numbers using method syntax
var evenNumbers = numbers.Where(n => n % 2 == 0);

foreach(var num in evenNumbers)
{
    Console.WriteLine(num); // Output: 2, 4, 6
}
```
| **Aspect** | **Detail** |
|---|---|
| **Pro** | More versatile and expressive. All LINQ operators (including single-result methods like `Max()`, `Any()`, `ToList()`) are available. |
| **Con** | Can become horizontally long and slightly less readable than Query Syntax when dealing with many chained clauses. |
