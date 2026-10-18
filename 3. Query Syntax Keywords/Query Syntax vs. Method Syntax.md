#### Query Syntax vs. Method Syntax

#### Shared data used in all examples

```csharp
record Employee(int Id, string Name, int DeptId, decimal Salary);
record Department(int Id, string Name);

var departments = new List<Department> {
    new(1, "IT"), new(2, "HR"), new(3, "Sales")
};

var employees = new List<Employee> {
    new(1, "Ali",   1, 5000), new(2, "Sara", 1, 6500),
    new(3, "Omar",  2, 4000), new(4, "Nour", 1, 5500),
    new(5, "Hana",  2, 4200)
};
```

#### 1. `orderby`

**Query syntax**
```csharp
var result = from e in employees
             orderby e.DeptId, e.Salary descending
             select e;
```

**Method syntax**
```csharp
var result = employees
    .OrderBy(e => e.DeptId)
    .ThenByDescending(e => e.Salary);
```

| Query syntax | Method syntax |
|---|---|
| `orderby x` | `OrderBy(e => x)` |
| `orderby x descending` | `OrderByDescending(e => x)` |
| `orderby x, y` | `OrderBy(...).ThenBy(...)` |
| `orderby x, y descending` | `OrderBy(...).ThenByDescending(...)` |

Common mistake: calling `OrderBy` twice. The second call discards the first sort. Use `ThenBy` for secondary keys.

#### 2. `group by`

**Query syntax**
```csharp
var result = from e in employees
             group e by e.DeptId into g
             select new {
                 DeptId = g.Key,
                 Count  = g.Count(),
                 Avg    = g.Average(x => x.Salary)
             };
```

**Method syntax**
```csharp
var result = employees
    .GroupBy(e => e.DeptId)
    .Select(g => new {
        DeptId = g.Key,
        Count  = g.Count(),
        Avg    = g.Average(x => x.Salary)
    });
```

| Query syntax | Method syntax | Meaning |
|---|---|---|
| `group e by e.DeptId` | `GroupBy(e => e.DeptId)` | Creates groups keyed by `DeptId` |
| `into g` | The lambda parameter `g` in `.Select(g => ...)` | Continues the query with the groups |
| `g.Key` | `g.Key` | The grouping key |
| `select new {...}` | `Select(g => new {...})` | Projects each group |

Output for the sample data:

| DeptId | Count | Avg |
|---|---|---|
| 1 | 3 | 5666.67 |
| 2 | 2 | 4100 |

#### 3. `join` (inner join)

**Query syntax**
```csharp
var result = from e in employees
             join d in departments on e.DeptId equals d.Id
             select new { e.Name, Dept = d.Name };
```

**Method syntax**
```csharp
var result = employees.Join(
    departments,
    e => e.DeptId,                        // outer key
    d => d.Id,                            // inner key
    (e, d) => new { e.Name, Dept = d.Name });  // result
```

| Query syntax part | Method syntax argument |
|---|---|
| `from e in employees` | The source you call `.Join` on (outer) |
| `join d in departments` | 1st argument: inner sequence |
| `e.DeptId` (left of `equals`) | 2nd argument: outer key selector |
| `d.Id` (right of `equals`) | 3rd argument: inner key selector |
| `select new {...}` | 4th argument: result selector |

In query syntax the key order matters: the outer key must be on the left of `equals`, the inner key on the right. Swapping them is a compile error.

#### 4. Bonus: left join

This is where query syntax is much easier to read.

**Query syntax**
```csharp
var result = from d in departments
             join e in employees on d.Id equals e.DeptId into emps
             from e in emps.DefaultIfEmpty()
             select new { Dept = d.Name, Employee = e?.Name ?? "(none)" };
```

**Method syntax**
```csharp
var result = departments
    .GroupJoin(employees, d => d.Id, e => e.DeptId,
               (d, emps) => new { d, emps })
    .SelectMany(x => x.emps.DefaultIfEmpty(),
                (x, e) => new { Dept = x.d.Name, Employee = e?.Name ?? "(none)" });
```

The `e?.Name` form works in LINQ to Objects. In EF Core queries, use `e == null ? "(none)" : e.Name` instead, since expression trees do not allow `?.`.

#### When to prefer which

| Situation | Better choice |
|---|---|
| Joins, left joins, multiple `from` clauses | Query syntax |
| Uses `let` for intermediate values | Query syntax |
| Simple filter, map, or sort | Method syntax |
| Needs `Take`, `Skip`, `Distinct`, `Count`, `First` | Method syntax |
| Mixing both | Allowed: wrap the query in parentheses and chain methods |

#### Practice exercises

Use the same `employees` and `departments` data. Solve each in both syntaxes.

| # | Task | Hint |
|---|---|---|
| 1 | List employee names ordered by salary, highest first | `orderby ... descending` |
| 2 | List employees with salary above 4500, sorted by name | `where` + `orderby` |
| 3 | Show each department name with its employee count | `join` + `group by` |
| 4 | Show the highest-paid employee in each department | `GroupBy` + `MaxBy` or `OrderByDescending(...).First()` |
| 5 | List all departments with their employees, including departments that have none | Left join (`DefaultIfEmpty`) |
| 6 | Show the top 2 earners overall, with their department names | `join` + `orderby` + `Take(2)` |
| 7 | Group employees by whether salary is above or below 5000 | `group e by e.Salary > 5000` |

