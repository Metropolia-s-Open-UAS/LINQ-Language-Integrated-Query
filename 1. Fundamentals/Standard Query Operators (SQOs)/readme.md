#### Standard Query Operators (SQOs)
- The Standard Query Operators (SQOs) are the foundational set of methods that form the core of LINQ. They are a collection of over 50 methods that provide common query capabilities like `filtering`, `projection`, `aggregation`, and `grouping`.
- These operators are implemented as Extension Methods on the interfaces that represent the data source:
     - `IEnumerable<T>`: Used for **LINQ to Objects** (in-memory collections).
     - `IQueryable<T>`: Used for **LINQ to Entities** (external data sources like databases).
- The methods share the same names (e.g., `Where`, `Select`), but their implementations differ based on the interface they extend:
     - `IEnumerable<T>`: methods execute client-side (in memory).
     - `IQueryable<T>`: methods build an Expression Tree that is translated into the native language of the data source (e.g., SQL) and executed server-side.





