# Language Integrated Query (LINQ)

Language-Integrated Query (LINQ) is a set of technologies based on the integration of query capabilities directly into the C# language.

Traditionally, queries against data are expressed as simple strings without type checking at compile time or IntelliSense support. Furthermore, you have to learn a different query language for each type of data source: SQL databases, XML documents, various Web services, and so on. With LINQ, a query is a first-class language construct, just like classes, methods, events.

For a developer who writes queries, the most visible "language-integrated" part of LINQ is the query expression. 

```CSharp
// Specify the data source.
int[] scores = { 97, 92, 81, 60 };

// Define the query expression.
IEnumerable<int> scoreQuery =
    from score in scores
    where score > 80
    select score;

// Execute the query.
foreach (int i in scoreQuery)
{
    Console.Write(i + " "); // output : 97 92 81

}
```

## Query expression overview

Query expressions can be used to query and to transform data from any LINQ-enabled data source. For example, a single query can retrieve data from a SQL database, and produce an XML stream as output.

The variables in a query expression are all strongly typed, although in many cases you do not have to provide the type explicitly because the compiler can infer it.

At compile time, query expressions are converted to Standard Query Operator method calls according to the rules set forth in the C# specification.

## How to enable LINQ querying of your data source

### In-memory data

There are two ways you can enable LINQ querying of in-memory data.

* If the data is of a type that implements `IEnumerable<T>`, you can query the data by using LINQ to Objects.
* If it does not make sense to enable enumeration of your type by implementing the `IEnumerable<T>` interface, you can define LINQ standard query operator methods in that type or create LINQ standard query operator methods that extend the type.

### Remote data

The best option for enabling LINQ querying of a remote data source is to implement the `IQueryable<T>` interface.

### IQueryable LINQ providers

LINQ providers that implement `IQueryable<T>` can vary widely in their complexity.

* **Less Complex Provider:** A less complex IQueryable provider might interface with a single method of a Web service.
* **Medium Complexity Provider:** An IQueryable provider of medium complexity might target a data source that has a partially expressive query language.
* **Complex Provider:** A complex IQueryable provider, such as the LINQ to SQL provider, might translate complete LINQ queries to an expressive query language, such as SQL.

## Standard Query Operators Overview in C#

### **LINQ Pattern**

LINQ pattern is formed by the methods that are standard query operators. These methods mainly operate on sequences where a sequence is an object whose type implements the `IEnumerable<T>` interface or the `IQueryable<T>` interface.

There are two sets of LINQ standard query operators:

1. Operating on objects of type `IEnumerable<T>`

2. Operating on objects of type `IQueryable<T>`

```csharp
// Example
var nums = new List<int>{ 1, 2, 3, 4, 5 };
var evens = nums.Where(n => n % 2 == 0);
```

### **Query Expression Syntax**

Some of the more frequently used standard query operators have dedicated C# and Visual Basic language keyword syntax that enables them to be called as part of a query expression.

### **Extending the Standard Query Operators**

Standard query operators can be extended by creating domain-specific methods that are suitable for the target domain or technology.

### **Obtain a Data Source**

In a LINQ query, the first step is to specify the data source. In C#, as in most programming languages, a variable must be declared before it can be used.

```csharp
// Example
var queryAllCustomers = from cust in customers
                        select cust;
```

### **Filtering**

The most common query operation is to apply a filter in the form of a Boolean expression. The filter returns only those elements for which the expression is true.

```csharp
// Example
var queryLondonCustomers = from cust in customers
                           where cust.City == "London"
                           select cust;
```

### **Ordering**

The `orderby` clause will cause the elements in the returned sequence to be sorted according to the default comparer for the type being sorted.

```csharp
// Example
var queryLondonCustomers3 =
    from cust in customers
    where cust.City == "London"
    orderby cust.Name ascending
    select cust;
```

### **Grouping**

The `group` clause enables you to group your results based on a key that you specify.

```csharp
// Example
var queryCustomersByCity =
      from cust in customers
      group cust by cust.City;
```

### **Joining**

Join operations create associations between sequences that are not explicitly modeled in the data sources.

```csharp
// Example
var innerJoinQuery =
    from cust in customers
    join dist in distributors on cust.City equals dist.City
    select new { CustomerName = cust.Name, DistributorName = dist.Name };
```

### **Selecting (Projections)**

The `select` clause produces the results of the query and specifies the "shape" or type of each returned element.

```csharp
// Example
var selectedCustomers =
    from cust in customers
    select new { Name = cust.Name, City = cust.City };
```

### **Query Expression Syntax Table**

This table lists the standard query operators that have equivalent query expression clauses.

| Method | C# query expression syntax |
| --- | --- |
| Cast | Use an explicitly typed range variable |
| GroupBy | group … by -or- group … by … into … |
| GroupJoin | join … in … on … equals … into … |
| Join | join … in … on … equals … |
| OrderBy | orderby |
| OrderByDescending | orderby … descending |
| Select | select |
| SelectMany | Multiple from clauses. |
| ThenBy | orderby …, … |
| ThenByDescending | orderby …, … descending |
| Where | where |

## **Writing Queries in C# (LINQ)**

### Create a C# Project

1. Launch Visual Studio.
2. Navigate to File > New > Project.
3. In the New Project dialog, go to Installed > Templates > Visual C# > Console Application.
4. Name your project or accept the default name and click OK.
5. Note that your project should have a reference to System.Core.dll and use the System.Linq namespace.

### Create an in-Memory Data Source

Use the following code to create a data source:

```csharp
public class Student
{
    public string First { get; set; }
    public string Last { get; set; }
    public int ID { get; set; }
    public List<int> Scores;
}

static List<Student> students = new List<Student>
{
    // Students data here...
};
```

### Create the Query

1. In the Main method, write a query to find students who scored more than 90 on their first test:

```csharp
IEnumerable<Student> studentQuery =
    from student in students
    where student.Scores[0] > 90
    select student;
```

### Execute the Query

Run the following loop to execute the query and print results:

```csharp
foreach (Student student in studentQuery)
{
    Console.WriteLine("{0}, {1}", student.Last, student.First);
}
```

### Modify the Query

1. Add a condition to filter students based on their scores:

```csharp
where student.Scores[0] > 90 && student.Scores[3] < 80  
```

2. Order the results alphabetically:

```csharp
orderby student.Last ascending  
```

or by their first test scores:

```csharp
orderby student.Scores[0] descending  
```

3. Modify the output:

```csharp
Console.WriteLine("{0}, {1} {2}", student.Last, student.First, student.Scores[0]);
```

4. Group results based on the first letter of their last name:

```csharp
IEnumerable<IGrouping<char, Student>> studentQuery2 =
    from student in students
    group student by student.Last[0];
```

5. Use var for implicit typing:

```csharp
var studentQuery3 = 
    from student in students
    group student by student.Last[0];
```

6. Order groups by their key:

```csharp
var studentQuery4 =
    from student in students
    group student by student.Last[0] into studentGroup
    orderby studentGroup.Key
    select studentGroup;
```

7. Introduce an identifier using let:

```csharp
var studentQuery5 =
    from student in students
    let totalScore = student.Scores.Sum()
    where totalScore / 4 < student.Scores[0]
    select student.Last + " " + student.First;
```

8. Combine query and method syntax:

```csharp
var studentQuery6 =
    from student in students
    let totalScore = student.Scores.Sum()
    select totalScore;

double averageScore = studentQuery6.Average();
```
