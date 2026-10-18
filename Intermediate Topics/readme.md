| **Topic** | **Key Idea** |
|---|---|
| **Anonymous types** | `select new { x.Name, x.Age }` |
| **Method chaining** | Combining operators fluently |
| **Custom comparers** | `IEqualityComparer<T>` for `Distinct`, `GroupBy`, etc. |
| **Select with index** | `Select((x, i) => ...)` |
| **SelectMany flattening** | One-to-many projection |
| **Left join** | `GroupJoin` + `DefaultIfEmpty` |
| **Composite keys** | `GroupBy(x => new { x.A, x.B })` |
| **Single vs. First** | `Single` throws if there is more than one match |
