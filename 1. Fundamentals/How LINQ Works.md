<img src="https://github.com/Metropolia-s-Open-UAS/media/blob/main/LINQ%20(Language%20Integrated%20Query)/how_linq_works_flow.png" alt="how_img_works">

## How each bullet maps to the diagram

| Your bullet | Where it appears |
|---|---|
| Unified querying | One query box at the top feeds both paths, whatever the source |
| Deferred execution | "Query object built" (nothing runs) and then the "Execution trigger" |
| Flexible syntax | Both syntaxes produce the same query object at the top |
| `IQueryable` and databases | The right branch: expression tree, translated to SQL, run on the server |
| Projection and transformation | The final box: only the selected fields come back |

## The two paths side by side

| Aspect | `IEnumerable<T>` path | `IQueryable<T>` path |
|---|---|---|
| Query stored as | Delegates (`Func<T, bool>`) | Expression trees (`Expression<Func<T, bool>>`) |
| Runs where | In your app's memory | In the database |
| Typical provider | LINQ to Objects | LINQ to Entities (EF Core) |
| Risk | Loading too much data into memory | Methods that cannot be translated to SQL |

