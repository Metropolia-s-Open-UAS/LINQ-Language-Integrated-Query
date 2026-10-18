#### Standard Query Operators (SQOs)
- The Standard Query Operators (SQOs) are the foundational set of methods that form the core of LINQ. They are a collection of over 50 methods that provide common query capabilities like `filtering`, `projection`, `aggregation`, and `grouping`.
- These operators are implemented as Extension Methods on the interfaces that represent the data source:
     - `IEnumerable<T>`: Used for **LINQ to Objects** (in-memory collections).
     - `IQueryable<T>`: Used for **LINQ to Entities** (external data sources like databases).
- The methods share the same names (e.g., `Where`, `Select`), but their implementations differ based on the interface they extend:
     - `IEnumerable<T>`: methods execute client-side (in memory).
     - `IQueryable<T>`: methods build an Expression Tree that is translated into the native language of the data source (e.g., SQL) and executed server-side.


| **Category** | **Purpose** | **Operators** | **Example / Notes** |
|---|---|---|---|
| **1. Filtering Operators** (Selecting a Subset) | Restrict the result set based on a condition, similar to SQL `WHERE`. | `Where()`, `OfType<TResult>()` | `employees.Where(e => e.IsActive && e.Salary > 70000)`; `OfType<TResult>()` filters elements by castability (e.g., get only `string` instances from a non-generic `ArrayList`). |
| **2. Projection Operators** (Shaping the Data) | Transform elements of a sequence into a new form, similar to SQL `SELECT`. | `Select()`, `SelectMany()` | `products.Select(p => new { p.Name, SalePrice = p.Price * 0.9 })` (anonymous type); `customers.SelectMany(c => c.Orders)` flattens all orders from all customers into one list. |
| **3. Ordering Operators** (Sorting the Results) | Sort the elements of a sequence. | `OrderBy()` / `OrderByDescending()`, `ThenBy()` / `ThenByDescending()`, `Reverse()` | `employees.OrderBy(e => e.LastName).ThenBy(e => e.FirstName)`; `ThenBy` is a secondary sort after a primary sort. |
| **4. Grouping Operators** | Group elements based on a common key. | `GroupBy()` | `orders.GroupBy(o => o.CustomerID)` returns a collection of `IGrouping<TKey, TSource>` objects. |
| **5. Set Operators** | Compare elements between two sequences based on set theory principles. | `Distinct()`, `Union()`, `Intersect()`, `Except()` | `Distinct()` = unique elements; `Union()` = unique from both; `Intersect()` = common to both; `Except()` = elements of first not in second. |
| **6. Quantifier Operators** (Boolean Checks) | Check if a condition is met and return a boolean; highly efficient as they usually stop processing once the result is determined. | `Any()`, `All()`, `Contains()` | `orders.Any(o => o.Status == "Pending")`; `grades.All(g => g >= 60)`; `Contains()` checks if a sequence contains a specified element. |
| **7. Aggregation Operators** (Calculating a Single Value) | Compute a single value from a sequence of values. | `Count()` / `LongCount()`, `Sum()`, `Min()` / `Max()`, `Average()` | Returns number of elements, sum, min/max value, or average. |
| **8. Partitioning Operators** (Paging) | Divide a sequence into two parts and return one; essential for paging. | `Skip()`, `Take()` | `data.Skip((pageNumber - 1) * pageSize).Take(pageSize)`; `Skip()` bypasses N elements; `Take()` returns N contiguous elements from the start. |
| **9. Element Operators** (Single Result) | Return a single element from a sequence. | `First()` / `FirstOrDefault()`, `Single()` / `SingleOrDefault()` | `FirstOrDefault()` returns default (e.g., `null`) if none found, avoiding an exception; `Single()` throws if zero or more than one element; `SingleOrDefault()` returns default if zero found. |



