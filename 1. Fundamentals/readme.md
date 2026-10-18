#### Introduction to LINQ
- LINQ is a major feature introduced in the .NET Framework 3.5 and C# 3.0 that revolutionized how data is queried in .NET applications.
#### What is LINQ?
- LINQ, or Language Integrated Query, is a powerful feature in .NET that allows querying and manipulating data collections directly in C#. It works with arrays, lists, XML, databases, and other data sources using a consistent, readable syntax.
#### Without LINQ vs. With LINQ

| **Approach** | **Code** |
|---|---|
| **Without LINQ** (Traditional Loop) | `List<Customer> nyCustomers = new List<Customer>();`<br>`foreach (var customer in allCustomers)`<br>`{`<br>`    if (customer.City == "New York")`<br>`    {`<br>`        nyCustomers.Add(customer);`<br>`    }`<br>`}` |
| **With LINQ** (Query Syntax) | `var nyCustomers = from customer in allCustomers`<br>`                  where customer.City == "New York"`<br>`                  // && customer.Orders.Any(o => o.OrderDate >= thirtyDaysAgo)`<br>`                  orderby customer.LastName`<br>`                  select customer;` |

> Before LINQ, querying data required different approaches for each data source: loops for lists, SQL for databases, and XML APIs for XML. This caused messy, hard-to-maintain code. LINQ solves this problem by providing a unified way to query any data in C# with less code and fewer errors.

<img src="https://github.com/Metropolia-s-Open-UAS/media/blob/main/LINQ%20(Language%20Integrated%20Query)/linq-works.webp" alt="linq work">
