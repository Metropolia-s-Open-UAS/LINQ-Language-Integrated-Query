### LINQ-Language-Integrated-Query
LINQ (Language Integrated Query) is a feature in C# that provides a way to query and manipulate data from different sources such as collections, databases, XML or objects. It integrates query capabilities directly into the C# language using a set of query operators and extension methods.

<img src="https://github.com/Metropolia-s-Open-UAS/media/blob/main/LINQ%20(Language%20Integrated%20Query)/why_use_linq_.webp" alt="Why Using LINQ?">

> LINQ provides a declarative, SQL-like syntax for filtering, sorting, grouping and transforming data.
```c#
using System;
using System.Linq;

class Program {
    static void Main() {
        int[] numbers = { 2, 5, 7, 8, 10 };

        // LINQ query to get numbers greater than 5 and double them
        var result = numbers.Where(n => n > 5).Select(n => n * 2);

        Console.WriteLine("Result of LINQ query:");
        foreach (var n in result) {
            Console.WriteLine(n);
        }
    }
}
```
```text
Output
Result of LINQ query:
14
16
20
```
##### LINQ Query flow
1. **Data Source** : It is the collection of elements on which the query will run. In code, int[] nums = { 2, 5, 7, 8, 10 } is the data source.
2. **Filtering** :  It is the process of selecting elements based on a condition. In code, Where(n => n > 5) filters numbers greater than 5.
3. **Projection** : It transforms each element into a new form. In code, Select(n => n * 2) doubles each filtered number.
4. **Execution** : The query actually runs when iterated. In code: The foreach loop executes the query and prints results.
> Note: **LINQ** supports both `query` syntax and `method (lambda)` syntax, making code readable, concise and consistent across data sources.

##### Architecture of LINQ
- LINQ follows a three-layered architecture:
<img src="https://github.com/Metropolia-s-Open-UAS/media/blob/main/LINQ%20(Language%20Integrated%20Query)/layer.webp" alt="linq layers">
