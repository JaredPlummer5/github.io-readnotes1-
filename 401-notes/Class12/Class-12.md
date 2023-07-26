# Entity Framework and APIs

Entity Framework (EF) is a wonderful tool in the .NET ecosystem. It helps developers work with data using objects of domain-specific classes without focusing too much on the underlying database tables and columns where this data is stored.

Let's understand it using a simple analogy. Imagine you're a child who wants to build a lego castle, but you only want to focus on how the castle will look, not how each lego block is made. Entity Framework is like your friend who brings you those lego blocks (the data from the database), so you can focus on building your castle (the application).

The way EF retrieves data from the database and converts it into objects that your program can use is through a process called Object-Relational Mapping (ORM).

## MVC with EF

Model-View-Controller (MVC) is a design pattern used in software development. It separates an application into three interconnected parts:

- The Model represents the data and the rules that govern access to and updates of this data. In EF, the model classes correspond to the entities (the lego blocks) in your database.
- The View displays the model data and sends user actions (e.g., button clicks) to the Controller.
- The Controller handles user input, works with the Model to perform operations on the data, and selects a View to display the updated model.

Here's an example of a model class in C#:

```csharp
public class LegoBlock
{
    public int Id { get; set; }
    public string Color { get; set; }
    public string Size { get; set; }
}
```

## Entity Framework Core

Entity Framework Core (EF Core) is a lightweight and extensible version of the original EF. It supports a variety of databases, including SQL Server, SQLite, MySQL, and others. With EF Core, you can do things like build models, query data, and save data back to the database.

## Data Seeding

Data seeding is like setting up your lego blocks before you start building. It's about adding initial data into your database. This could be things like default users or roles, test data for development, or any data your application expects to exist.

Here's an example of data seeding in EF Core:

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<LegoBlock>().HasData(
        new LegoBlock { Id = 1, Color = "Red", Size = "Large" },
        new LegoBlock { Id = 2, Color = "Blue", Size = "Small" }
    );
}
```

## User Secrets

Just like you might have secret hiding places for your special toys, your app can have secrets too. User Secrets are a way to store confidential data (like database connection strings, API keys, etc.) without having them in your code. This makes sure your secrets don't end up in source control and potentially become public.

Here's an example of how to use user secrets in ASP.NET Core:

```csharp
var builder = new ConfigurationBuilder();
builder.AddUserSecrets<Startup>();
Configuration = builder.Build();
```

After adding user secrets to the configuration, you can use it like this:

```csharp
var secret = Configuration["MySecret"];
```

Remember to keep your secrets safe, just like you keep your special toys!

## APIs

APIs (Application Programming Interfaces) are like the instructions for your lego set. They define how different pieces (applications) should communicate and work together. An API is the part of the server that receives requests and sends responses.

With Entity Framework and MVC, we can easily build APIs to perform CRUD (Create, Read, Update, Delete) operations. For example, the code below creates an API endpoint that fetches all the lego blocks (from our previous examples) from the database:

```csharp
[HttpGet]
public async Task<ActionResult<IEnumerable<LegoBlock>>> GetLegoBlocks()
{
    return await _context.LegoBlocks.ToListAsync();
}
```

To use this API, someone would make a 'GET' request to your API's URL, and they would get a list of lego blocks in response.
