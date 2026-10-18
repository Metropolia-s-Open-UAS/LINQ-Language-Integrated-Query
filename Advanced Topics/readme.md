| **Topic** | **Key Idea** |
|---|---|
| **Expression trees** | `Expression<Func<T,bool>>`, code as data |
| **Building dynamic queries** | Composing predicates, `PredicateBuilder`, `System.Linq.Dynamic.Core` |
| **Custom LINQ operators** | Extension methods on `IEnumerable<T>` with `yield return` |
| **Performance** | Avoid multiple enumeration, use `Any()` instead of `Count() > 0` |
| **N+1 problem (EF)** | Use `Include` / `ThenInclude` or projection |
| **Tracking vs. no-tracking** | `AsNoTracking()` for read-only queries |
| **Client vs. server evaluation** | Which parts run in the DB vs. in memory |
| **Compiled queries** | `EF.CompileQuery` for repeated queries |
| **PLINQ** | `AsParallel`, `WithDegreeOfParallelism`, `AsOrdered` |
| **Async LINQ** | `System.Linq.Async`, `IAsyncEnumerable<T>`, `ToListAsync()` |
