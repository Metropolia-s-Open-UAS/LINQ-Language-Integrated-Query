#### LINQ API in .NET
- We can write LINQ queries for the classes that implement `IEnumerable<T>` or `IQueryable<T>` interface. The `System.Linq` namespace includes the following classes and interfaces require for LINQ queries.
> `System.Linq namespace` is included by default when you add a new class in Visual Studio.

- LINQ queries uses extension methods for classes that implement IEnumerable or IQueryable interface. The Enumerable and Queryable are two static classes that contain extension methods to write LINQ queries.
  
| **Aspect** | **Enumerable Class** | **Queryable Class** |
|---|---|---|
| **Definition** | Includes extension methods for classes that implement the `IEnumerable<T>` interface. | Includes extension methods for classes that implement the `IQueryable<T>` interface. |
| **Target Interface** | `IEnumerable<T>` | `IQueryable<T>` |
| **Data Sources** | All built-in collection classes that implement `IEnumerable<T>`. | Specific data sources where the type of data is known (e.g., databases via Entity Framework). |
| **Usage** | Write LINQ queries to retrieve data from built-in collections. | Provides querying capabilities against a specific data source. |
| **Example** | LINQ queries over in-memory collections (lists, arrays, etc.). | Entity Framework API implements `IQueryable<T>` to support LINQ queries with underlying databases such as MS SQL Server. |
| **Third-Party Support** | — | APIs exist for third-party data (e.g., LINQ to Amazon implements `IQueryable` to query Amazon web services for books and other items). |
| **Extension Methods** | Available for generic collections in C# or VB.NET. | Available for use with various native or third-party data providers. |

