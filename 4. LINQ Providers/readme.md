#### LINQ Providers 

#### The Five LINQ Providers

| **#** | **Provider** | **Also Known As** |
|---|---|---|
| 1 | LINQ to Objects | — |
| 2 | LINQ to XML | XLINQ |
| 3 | LINQ to SQL | DLINQ |
| 4 | LINQ to DataSets | — |
| 5 | LINQ to Entities | — |

#### Provider Details

| **Provider** | **Purpose / Description** | **Execution Model** | **Key Requirements / Notes** | **Example** |
|---|---|---|---|---|
| **LINQ to Objects** | Allows .NET developers to write "queries" over collections of objects. Generated code refers to standard query operator implementations as defined on the Sequence pattern, allowing `IEnumerable<T>` collections to be queried locally. Represents a new approach to collections: declarative code describing *what* to retrieve instead of complex `foreach` loops specifying *how*. | **Local** (in-memory) execution engine. | Works on `IEnumerable<T>` collections. | `IEnumerable<int> firstFourNumbers = integers.Take(4);` — takes the first four integers from the collection. |
| **LINQ to XML (XLINQ)** | Converts an XML document to a collection of `XElement` objects, which are then queried using the local execution engine provided by the standard query operator implementation. Allows creating, reading, and editing XML files in an easy, understandable way. | **Local** (in-memory) execution engine. | Add a reference to `System.Xml.Linq.dll` (for `XDocument` and other classes) and use the `System.Linq` namespace (for LINQ syntax). | — |
| **LINQ to SQL (DLINQ)** | Provides a runtime infrastructure for managing relational data as objects without losing the ability to query. The application can manipulate objects while LINQ to SQL tracks changes automatically in the background. | **Does NOT use the LINQ query engine** — converts a LINQ query to a **SQL query** sent to **SQL Server** for processing. | Mapping is done by defining classes that correspond to database tables (using `[Table]` and `[Column]` attributes). | `[Table(Name="Customers")] public class Customer { [Column(IsPrimaryKey = true)] public int CustID; [Column] public string CustName; }` |
| **LINQ to DataSets** | Makes it easier and faster to query data cached in a `DataSet` object. Simplifies querying by enabling developers to write queries from the programming language itself instead of a separate query language. Allows use of superior LINQ querying features in legacy applications **without rewriting the whole data access layer**. | Querying over data cached in a `DataSet`. | Useful for legacy applications; no full data-access-layer rewrite needed. | — |
| **LINQ to Entities** | Provides LINQ support enabling developers to write queries against the **Entity Framework conceptual model** using VB or C#. Queries are represented by **command tree queries** that execute against the object context. Converts LINQ queries to command tree queries, executes them against the Entity Framework, and returns objects usable by both EF and LINQ. | Executes against the **object context** (command tree queries). | Uses `ObjectQuery` / `ObjectContext`. | — |

#### LINQ to Entities — Query Creation & Execution Process

| **Step** | **Action** |
|---|---|
| **1** | Construct an `ObjectQuery` instance from `ObjectContext`. |
| **2** | Compose a LINQ to Entities query in C# or Visual Basic using the `ObjectQuery` instance. |
| **3** | Convert LINQ standard query operators and expressions to **command trees**. |
| **4** | Execute the query (in command tree representation) against the data source. Any exceptions thrown on the data source during execution are passed directly up to the client. |
| **5** | Return query results back to the client. |
