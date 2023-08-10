# Create Data Transfer Objects (DTOs)

## Introduction

- The article discusses the use of Data Transfer Objects (DTOs) in web API.
- DTOs are used to change the shape of the data sent to the client.
- Reasons to use DTOs include removing circular references, hiding properties, reducing payload size, flattening object graphs, avoiding over-posting vulnerabilities, and decoupling service and database layers.

## Creating DTO Classes

- Two DTO classes are created for the Book entity: `BookDto` and `BookDetailDto`.
- `BookDto` contains a subset of properties from `BookDetailDto`.

```csharp
namespace BookService.Models
{
    public class BookDto
    {
        public int Id { get; set; }
        public string Title { get; set; }
        public string AuthorName { get; set; }
    }
}

namespace BookService.Models
{
    public class BookDetailDto
    {
        public int Id { get; set; }
        public string Title { get; set; }
        public int Year { get; set; }
        public decimal Price { get; set; }
        public string AuthorName { get; set; }
        public string Genre { get; set; }
    }
}
```

## Modifying Controller Methods

- The GET methods in the `BooksController` class are replaced with versions that return DTOs.
- LINQ Select statement is used to convert from Book entities into DTOs.

```csharp
// GET api/Books
public IQueryable<BookDto> GetBooks()
{
    var books = from b in db.Books
                select new BookDto()
                {
                    Id = b.Id,
                    Title = b.Title,
                    AuthorName = b.Author.Name
                };

    return books;
}

// GET api/Books/5
[ResponseType(typeof(BookDetailDto))]
public async Task<IHttpActionResult> GetBook(int id)
{
    var book = await db.Books.Include(b => b.Author).Select(b =>
        new BookDetailDto()
        {
            Id = b.Id,
            Title = b.Title,
            Year = b.Year,
            Price = b.Price,
            AuthorName = b.Author.Name,
            Genre = b.Genre
        }).SingleOrDefaultAsync(b => b.Id == id);
    if (book == null)
    {
        return NotFound();
    }

    return Ok(book);
}
```

#### Modifying Post Method

- The `PostBook` method is modified to return a DTO.

```csharp
[ResponseType(typeof(BookDto))]
public async Task<IHttpActionResult> PostBook(Book book)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }

    db.Books.Add(book);
    await db.SaveChangesAsync();

    // New code:
    // Load author name
    db.Entry(book).Reference(x => x.Author).Load();

    var dto = new BookDto()
    {
        Id = book.Id,
        Title = book.Title,
        AuthorName = book.Author.Name
    };

    return CreatedAtRoute("DefaultApi", new { id = book.Id }, dto);
}
```

#### Note

- The tutorial demonstrates manual conversion to DTOs.
- Libraries like [AutoMapper](http://automapper.org/) can be used for automatic conversion.

Certainly! Here are the markdown notes for the article titled "How to use Data Transfer Objects in ASP.NET Core 3.1" from InfoWorld. You can find the full article [here](https://www.infoworld.com/article/3562271/how-to-use-data-transfer-objects-in-aspnet-core-31.html).

## How to use Data Transfer Objects in ASP.NET Core 3.1

### Introduction

- A Data Transfer Object (DTO) is an instance of a POCO (plain old CLR object) class used to encapsulate data.
- DTOs are used to decouple clients from internal data structures.
- This article explains how to work with DTOs in ASP.NET Core 3.1.

### Creating an ASP.NET Core 3.1 API Project

- Launch Visual Studio 2019.
- Create a new ASP.NET Core API project.
- Select .NET Core as the runtime and ASP.NET Core 3.1 from the drop-down list.
- Select "API" as the project template.
- Ensure that "Enable Docker Support" and "Configure for HTTPS" are unchecked.
- Set Authentication as "No Authentication."

### Why Use Data Transfer Objects (DTOs)?

- **Decoupling Layers**: DTOs decouple the presentation layer from the service layer.
- **Data Hiding**: DTOs allow you to return only the requested data, hiding unnecessary details.
- **Bandwidth Efficiency**: DTOs are lightweight and suitable for bandwidth-constrained mediums.
- **Abstraction**: DTOs abstract the domain objects from the user interface.

### Creating Model and DTO Classes

- Create an `Employee` model class with properties like `Id`, `FirstName`, `LastName`, `DepartmentName`, `Basic`, `DA`, `HRA`, and `NetSalary`.
- Create a DTO class `EmployeeDTO` with only the necessary properties like `Id`, `FirstName`, `LastName`, and `DepartmentName`.

```csharp
public class Employee  
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string DepartmentName { get; set; }
    public decimal Basic { get; set; }
    public decimal DA { get; set; }
    public decimal HRA { get; set; }
    public decimal NetSalary { get; set; }
}

public class EmployeeDTO  
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string DepartmentName { get; set; }
}
```

#### Converter Class

- You may create a converter class to convert between the `Employee` model class and the `EmployeeDTO`.
- Alternatively, you can use AutoMapper, a popular object-to-object mapping library.

#### Conclusion

- DTOs are essential in designing applications to ensure proper encapsulation, data hiding, and decoupling of layers.
- They are particularly useful in API development and scenarios where bandwidth efficiency is crucial.

(Note: The content has been processed for brevity, and this is the first part of the article. There may be more details and code snippets in the subsequent sections.)

Please let me know if you would like me to continue and retrieve the remaining parts of the article!
