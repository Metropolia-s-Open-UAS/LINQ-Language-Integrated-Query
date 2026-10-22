#### LINQ Architecture Diagram: Explained
<img src="https://github.com/Metropolia-s-Open-UAS/media/blob/main/LINQ%20(Language%20Integrated%20Query)/linq.webp">

#### Layer by layer

| Layer | In the image | Role |
|---|---|---|
| Top: languages | C#, VB.NET, Other Languages | The .NET languages that can write LINQ queries |
| Middle: LINQ engine | .NET Language Integrated Query (LINQ) | The common query layer: operators like `Where`, `Select`, `GroupBy`, with the same syntax for every language |
| Bottom: data sources | LINQ-Enabled Data Sources (green box) | The providers that connect LINQ to actual data |

#### The bottom layer in detail

| Box | Data it works with | Belongs to ADO.NET? |
|---|---|---|
| LINQ to Objects | In-memory collections (arrays, `List<T>`) | No |
| LINQ to Datasets | `DataSet`, `DataTable` | Yes |
| LINQ to SQL | SQL Server databases | Yes |
| LINQ to Entities | Entity Framework models | Yes |
| LINQ to XML | `XDocument`, `XElement` | No |

The blue box in the middle (LINQ-Enabled ADO.NET) groups the three providers that sit on top of ADO.NET database technology. LINQ to Objects and LINQ to XML are outside it because they do not talk to a database.

#### How to read the flow

| Direction | Meaning |
|---|---|
| Top to middle | Any .NET language writes a query using the same LINQ operators |
| Middle to bottom | LINQ hands the query to the right provider for the data source |
| Provider to data | The provider translates the query into what the source understands (delegates, SQL, XML traversal) |

This is why the same `Where(x => x.Age > 18)` works on a list, a database table, or an XML file.

<img src="https://github.com/Metropolia-s-Open-UAS/media/blob/main/LINQ%20(Language%20Integrated%20Query)/linq_architecture_modern.png">
