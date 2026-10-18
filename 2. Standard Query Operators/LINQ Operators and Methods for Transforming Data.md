#### LINQ Operators and Methods for Transforming Data — Tabulated Summary

#### Overview

| **Topic** | **Detail** |
|---|---|
| **Definition** | LINQ provides a rich set of query operators in C# to query and manipulate data from collections, arrays, or databases in a type-safe and expressive way. |
| **Operator Categories** | Transforming, Restriction, Partitioning, and Set operators. |

#### 1. Transforming Operators

| **Operator** | **Purpose** | **Behavior** | **Example** | **Output** |
|---|---|---|---|---|
| **Select** | Projects each element of a sequence into a new form. | Preserves the number of elements but can change their type or structure. | `var squaredNumbers = numbers.Select(x => x * x);` on `{1,2,3,4,5}` | `1, 4, 9, 16, 25` |
| **SelectMany** | Flattens a sequence of collections into a single sequence. | Useful for one-to-many projections. | `var flattenedNumbers = numbers.SelectMany(x => x);` on `{{1,2,3},{4,5,6},{7,8,9}}` | `1,2,3,4,5,6,7,8,9` |

#### 2. Restriction Operator

| **Operator** | **Purpose** | **Behavior** | **Example** | **Output** |
|---|---|---|---|---|
| **Where** | Filters elements based on a condition. | Restricts the result set to elements matching the predicate. | `var evenNumbers = numbers.Where(x => x % 2 == 0);` on `{1..9}` | `2, 4, 6, 8` |
#### 3. Partitioning Query Operators

> Return a specified number of elements from the start of a LINQ query, or while a condition is true.

| **Operator** | **Purpose** | **Behavior** | **Example** | **Output** |
|---|---|---|---|---|
| **Take** | Returns the output sequence with a specified number of elements from the start of the query. | Returns first N elements. | `numbers.Take(3)` on `{1..9}` | `1, 2, 3` |
| **TakeWhile** | Returns elements from the start of the query while a specified condition is matched. | Stops at first element failing the predicate. | `numbers.TakeWhile(x => x < 4)` on `{1..9}` | `1, 2, 3` |
| **Skip** | Returns the output sequence that skips/ignores a specified number of elements from the start of the query. | Skips first N elements. | `numbers.Skip(3)` on `{1,2,3,4,5}` | `4, 5` |
| **SkipWhile** | Returns the output sequence that skips elements at the start of the query while the given predicate is matched. | Skips until predicate fails, then returns the rest. | `numbers.SkipWhile(x => x < 4)` on `{1,2,3,4,5}` | `4, 5` |
#### 4. Set Operator

| **Operator** | **Purpose** | **Behavior** | **Example** | **Output** |
|---|---|---|---|---|
| **Distinct** | Removes duplicate elements from a sequence. | Uses default or a custom equality comparer; returns only unique elements. | `numbers.Distinct()` on `{1,1,2,2,3,3,4,5}` | `1, 2, 3, 4, 5` |
