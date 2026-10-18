#### LINQ Query Syntax: Summary

#### Core idea

| Point | Explanation |
|---|---|
| Definition | A SQL-like way to write LINQ queries directly in C# (also called query expression syntax) |
| Keywords | `from`, `where`, `select`, `group`, `orderby`, `join`, `let` |
| Works on | Any `IEnumerable<T>` or `IQueryable<T>` source: collections, arrays, XML, databases |
| Benefit | Readable and type-safe, with no separate query language |

#### The four steps

| Step | What to do | Code |
|---|---|---|
| 1. Namespace | Import LINQ | `using System.Linq;` |
| 2. Data source | Create the collection | `List<string> my_list = new List<string>() { ... };` |
| 3. Query | Write it with query keywords | `var res = from l in my_list where l.Contains("my") select l;` |
| 4. Execution | Enumerate the result | `foreach (var q in res) { Console.WriteLine(q); }` |

#### Anatomy of the query

```csharp
var res = from l in my_list
          where l.Contains("my")
          select l;
```

| Part | Role |
|---|---|
| `res` | Query variable. It holds the query, not the results. |
| `from l in my_list` | Names the data source (`my_list`) and the range variable (`l`) |
| `l` | Range variable, which stands for one element at a time |
| `where l.Contains("my")` | Filter: keeps strings containing "my" |
| `select l` | Projection: defines what is returned (here, the string itself) |

#### Trace of the example

| Item in `my_list` | Contains "my"? | In output? |
|---|---|---|
| `This is my Dog` | Yes | Yes |
| `Name of my Dog is Robin` | Yes | Yes |
| `This is my Cat` | Yes | Yes |
| `Name of the cat is Mewmew` | No | No |

The last string has "Mew**mew**" but no lowercase "my", and `Contains` is case-sensitive by default.

#### Notes beyond the article

| Note | Detail |
|---|---|
| Deferred execution | `res` is only a query. It runs at the `foreach`, so changes to `my_list` before that line appear in the output. |
| Method syntax equivalent | `my_list.Where(l => l.Contains("my"))` gives the same result. The compiler turns query syntax into method calls. |
| Case-insensitive search | `l.Contains("my", StringComparison.OrdinalIgnoreCase)` |
| Must end with `select` or `group` | A query expression always finishes with one of them (the method-syntax `Where` alone does not need `select`). |
| Query syntax limits | Operators like `Count`, `First`, `Take`, `Skip` and `Distinct` have no keyword. You wrap the query in parentheses and call them as methods, e.g. `(from ... select ...).Count()`. |

