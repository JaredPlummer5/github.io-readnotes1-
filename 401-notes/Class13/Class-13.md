# Dependency Injection, Repository Pattern, Repository Design Pattern, SOLID Principles, Why SOLID Matters & SOLID Principles in Pictures

1. **Overview of Dependency Injection**

   Dependency Injection (DI) is a technique that makes an application flexible, testable and loosely coupled. It's like giving a toy car to a child, the child doesn't need to know how the car was made or how it works, they just play with it. In coding, if an object needs another object, it gets it from an external source (like a service container in ASP.NET Core), not create it by itself.

2. **Register groups of services with extension methods**

   Think of this as having a box of different toys (services) and we label (register) each toy in the box. With extension methods, we can add multiple toys (services) in the box at once. Here's an example in code:

   ```csharp
   public static class MyServiceCollectionExtensions
   {
       public static IServiceCollection AddMyServices(this IServiceCollection services)
       {
           services.AddScoped<Service1>();
           services.AddSingleton<Service2>();
           services.AddTransient<Service3>();
           return services;
       }
   }
   ```
   In `Startup.ConfigureServices`, you can then call `services.AddMyServices();` to add all these services at once.

3. **Service Lifetimes**

   ASP.NET Core has three types of lifetimes for services:

   - **Transient**: Like a bubble machine, every time you ask for a bubble (service), you get a new one. Transient services are created each time they're requested.
   - **Scoped**: Like a pet, you get the same pet (service) within a certain area (scope), such as within a single HTTP request.
   - **Singleton**: Like a family car, everyone in the family uses the same car (service). Singleton services are created the first time they're requested and then every subsequent request uses the same instance.

4. **Service registration methods**

   These are the methods we use to tell ASP.NET Core about our services (or toys). Here's how we do it:

   ```csharp
   services.AddTransient<MyService>(); // Register a transient service
   services.AddScoped<MyService>(); // Register a scoped service
   services.AddSingleton<MyService>(); // Register a singleton service
   ```

5. **Constructor injection behavior**

   Constructor injection is like having a toy-making machine, where you put in some parts (dependencies), and it gives you a toy (service). When creating a service, ASP.NET Core can automatically provide the required services if you ask for them in the constructor. For example:

   ```csharp
   public class MyService
   {
       private readonly OtherService _otherService;

       public MyService(OtherService otherService)
       {
           _otherService = otherService; // otherService is injected by ASP.NET Core
       }
   }
   ```

Certainly! Here's the continuation of the explanation:

6. **Lifetime and registration options**

   Just like we need to know how long a toy will last, we need to decide how long a service will live. This is determined when we register the service using `AddTransient`, `AddScoped`, or `AddSingleton`. We can also decide if the service will be created by a factory function or if we'll provide an instance directly.

7. **Resolve a service at app start up**

   This is like asking for a toy as soon as you walk into a toy shop. We can get a service as soon as the application starts by asking for it in the `Configure` method in Startup class:

   ```csharp
   public void Configure(IApplicationBuilder app, MyService myService)
   {
       // Use myService here...
   }
   ```

8. **Scope validation**

   This is a way of checking that the services are being used correctly. For example, if a singleton service tries to use a scoped service, it's like trying to bring a pet (which belongs at home) to school. This isn't allowed because the pet might not behave properly at school. We can turn on scope validation to prevent this:

   ```csharp
   public static IHostBuilder CreateHostBuilder(string[] args) =>
       Host.CreateDefaultBuilder(args)
           .UseDefaultServiceProvider(options =>
               options.ValidateScopes = true)
           .ConfigureWebHostDefaults(webBuilder =>
               webBuilder.UseStartup<Startup>());
   ```

9. **Request Services**

   Once you're in the toy store, you can ask for specific toys. In the same way, once a request is being processed, your controller actions can ask for services. This is done by including the service as a parameter in the action method:

   ```csharp
   public IActionResult Index(MyService myService)
   {
       // Use myService here...
       return View();
   }
   ```

Sure! Let's continue with the list:

10. **Design services for dependency injection**

    Services should be designed in a way that they can easily accept their dependencies through their constructors (or sometimes properties). This is like creating toys with batteries included. If a toy needs batteries to operate, we design it in a way that batteries can be easily inserted into it.

11. **Disposal of services**

    Just as we teach kids to clean up their toys after playing, in programming we need to clean up services when they are no longer needed. Services that implement `IDisposable` will be disposed at the end of the request (for scoped services) or at the end of the application (for singleton services).

    ```csharp
    public class MyService : IDisposable
    {
        public void Dispose()
        {
            // Clean up here...
        }
    }
    ```

12. **Services not created by the service container**

    These are services that are created manually, not by the DI container. It's like buying a toy from another store, not from the one you are currently in. You can still play with it, but the store won't know about it, and it won't be able to fix it if it breaks.

13. **IDisposable guidance for Transient and shared instances**

    Transient services (like bubbles) are created and disposed each time they are used. But if a transient service is used by a singleton service, it's like keeping a bubble in your pocket. The bubble might pop (the service might be disposed) while you still need it. So we have to be careful when using transient services in singleton services.

14. **Default service container replacement**

    ASP.NET Core comes with a built-in DI container (like a toy box that comes with the room). But if you don't like this box, you can replace it with your own box. There are many third-party DI containers you can use, but be aware that changing the box might cause some toys to behave differently.

    ```csharp
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        // Add services...

        var container = new SomeOtherContainer(services);
        return container;
    }
    ```

## The Repository Pattern

### Overview

Imagine you have a toy box where you keep all your toys. Every time you want a toy, you go to the toy box, find it, and take it out. When you're done playing, you put it back in the box. The Repository Pattern is like that toy box for our data or information in a software program.

### One Repository Per Aggregate

Think of 'aggregate' as a group of toys that belong together - like a set of Lego blocks that make a castle. Just as we keep that set of Legos together in a special box, we keep all the related data together in one repository. We don't make a repository for each piece of data, but for each group of related data.

```csharp
public interface IRepository<T> where T : IAggregateRoot
{
    T Add(T aggregate);
    // ...
}
```

### Enforce One Aggregate Root Per Repository

Let's say our Lego set has a special 'key' block without which the castle can't be built. In our program, this is called an 'aggregate root'. We make sure that we have one 'key' block for each Lego set, and similarly, we have one aggregate root for each repository.

```csharp
public interface IOrderRepository : IRepository<Order>
{
    Order Add(Order order);
    // ...
}
```

### Repository Pattern Makes Testing Easier

Testing our software program is like doing a trial run of building our Lego castle. Just as we would first try to build the castle without using glue, we test our program without the real data. The repository pattern lets us easily replace the real data with some make-believe data for testing, just like using dummy blocks instead of the real Lego.

### Difference Between Repository Pattern and Data Access Class (DAL)

The Repository pattern is like a smart toy box that not only stores our toys but also knows how to sort and manage them. The Data Access Layer (DAL), on the other hand, is like a simple box that just stores toys without any additional features.

### Implementing Unit of Work

The Unit of Work is like the rule that says "pick up all your Lego blocks at once when you're done playing". It means that we handle all our data operations together as a single unit or 'transaction', instead of doing them separately.

```csharp
public class UnitOfWork : IUnitOfWork
{
    private readonly DbContext context;

    public UnitOfWork(DbContext context)
    {
        this.context = context;
    }

    public void Commit()
    {
        context.SaveChanges();
    }
    // ...
}
```

### Repositories Shouldn't Be Mandatory

Remember that having a toy box is handy but not mandatory. You can still play with your toys even if you don't have a toy box. Similarly, while repositories can be useful, they're not mandatory for writing a software program.

### Key Takeaways

The Repository Pattern helps us manage and organize our data just like a toy box helps us manage and organize our toys. It helps us keep related data together, makes testing easier, and allows us to handle all our data operations together as a single unit. However, just like a toy box, it's a helpful tool but not mandatory.

## The Repository Pattern

The repository pattern is a way to organize our code so that the business logic and data access are separate. This makes our code cleaner, easier to maintain, and easier to test.

We can think of it like a librarian. A librarian doesn't care about where the books are stored, they only care about how to get, update, create or delete a book. That's what the repository pattern does!

### Data Access Objects (DAO)

DAO is a common way to interact with our data layer. It's a set of methods that let us do things like read, update, create, or delete data. 

```csharp
public interface IArticleDao
{
    List<Article> ReadAll();

    List<Article> ReadLatest();

    List<Article> ReadByTags(params Tag[] tags);

    Article ReadById(long id);

    Article Create(Article article);

    Article Update(Article article);

    Article Delete(Article article);
}
```

Think of it like a big machine that has different buttons (methods). Each button does a different thing with the articles - one button to read all articles, one to read the latest ones, and so on.

But DAOs are usually closely tied with databases, and if you want to keep your application flexible, you might want to use something else, like the repository pattern.

### Abstraction

The repository pattern allows us to abstract away the specifics of how we access data. This means we can change where our data comes from without changing the rest of our code.

```csharp
public interface IRepository<T>
{
    List<T> ReadAll();

    T Read(Criteria criteria);
    
    T Create(T entity);
    
    T Update(T entity);
    
    T Delete(T entity);
}

```
We can think of this like a remote control that can control any TV, not just a specific model.

However, the `read(Criteria criteria)` method can be tricky. Different implementations (like an in-memory database or a SQL database) may need different types of Criteria. So, we need a compromise.

### Compromise

To keep the benefits of the repository pattern without having to create a complex Criteria system, we can add a `readById(K id)` method to our Repository interface. This allows us to find specific items without needing a complex Criteria.

```csharp
public interface IRepository<T, K>
{
    List<T> ReadAll();

    T ReadById(K id);
    
    T Create(T entity);
    
    T Update(T entity);
    
    T Delete(T entity);
}

```

### Criteria

Sometimes, we need to get specific subsets of data from our repository. Instead of creating a complex Criteria system, we can create additional methods in a new interface that extends our basic Repository. This gives us specific, easy-to-understand methods without breaking our abstraction.

```csharp
public interface IArticleRepository : IRepository<Article, long>
{
    List<Article> ReadAll();
    
    Article ReadById(long id);
    
    Article Create(Article article);
    
    Article Update(Article article);
    
    Article Delete(Article article);
    
    List<Article> ReadLatest();
    
    List<Article> ReadByTags(params Tag[] tags);
}

```

## Test-Driven Development (TDD) and SOLID Principles with C#

This series of posts will cover the basics of Test-Driven Development (TDD) and SOLID principles, aiming to help you transition from a novice to a functional TDD developer. Let's dive into the SOLID principles now.

### Is Your Code SOLID?

SOLID is an acronym for five design principles introduced by Robert C. Martin, popularly known as "Uncle Bob", to make software designs more understandable, flexible, and maintainable. 

#### 1. Single Responsibility Principle (SRP)

The SRP dictates that a class should have only one reason to change, meaning it should only have one job.

Let's look at an example. 

```csharp
public class ShoppingCart
{
    public List<Product> Products { get; set; }
    
    // This is the only job of ShoppingCart, adding products.
    public void AddProduct(Product product)
    {
        Products.Add(product);
    }
}
```

This `ShoppingCart` class has only one job: to hold a collection of products. If we want to introduce functionality related to a loyalty rewards program, we'd create a separate class, not complicate the `ShoppingCart` class.

Tests that adhere to SRP are simpler and more straightforward. Each test should check only one thing. If a test fails, you know exactly where to look.

#### 2. Open/Closed Principle (OCP)

The OCP states that software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification. You should be able to add new functionality without changing the existing code.

```csharp
public class Rectangle
{
    public virtual double Height { get; set; }
    public virtual double Width { get; set; }
}

public class Square : Rectangle
{
    private double _side;
    
    public override double Height 
    { 
        get { return _side; }
        set { _side = value; }
    }

    public override double Width 
    { 
        get { return _side; }
        set { _side = value; }
    }
}
```

In this example, the `Square` class extends the `Rectangle` class without changing its structure. The `Rectangle` class is "closed for modification" but "open for extension".

#### 3. Liskov Substitution Principle (LSP)

The LSP states that if a program is using a base class, it should be able to use any of its subclasses without the program knowing or breaking.

Let's take an example. 

```csharp
public class Bird
{
    public virtual void Fly()
    {
        // Code for bird to fly
    }
}

public class Sparrow : Bird
{
    public override void Fly()
    {
        // Code for sparrow to fly
    }
}

public class Penguin : Bird
{
    public override void Fly()
    {
        // Penguins can't fly, so this is a violation of LSP
    }
}
```

In the above code, `Penguin` is a type of `Bird`, but it cannot fly. So `Penguin` can't replace `Bird` without affecting the behavior, which violates the LSP.

#### 4. Interface Segregation Principle (ISP)

ISP states that no client should be forced to depend on methods it does not use. It's better to have many smaller interfaces than one large interface.

```csharp
public interface ILoan
{
    void ApproveLoan();
}

public interface ISecuredLoan : ILoan
{
    void MortgageProperty();
}

public interface IUnsecuredLoan : ILoan
{
    void CheckCreditHistory();
}
```

In this example, there are different interfaces for different types of loans. Clients interested in secured loans don't need to know about credit history checks and vice versa.

#### 5. Dependency Inversion Principle (DIP)

DIP advises that high-level modules should not depend on low-level modules. Both should depend on abstractions. Moreover, abstractions should not depend on details. Details should depend on abstractions.

```csharp
public interface IDatabase
{
    void Add();
}

public class SqlDatabase : IDatabase
{
    public void Add()
    {
        // Code to add in SQL Database
    }
}

public class Employee
{
    private IDatabase _database;
    
    public Employee(IDatabase database)
    {
        _database = database;
    }
    
    public void Add()
    {
        _database.Add();
    }
}
```

Here, the `Employee` class is not dependent on a specific database type. Instead, it's dependent on an abstraction (`IDatabase`). We can use any database that implements `IDatabase`, making the code more flexible and easy to maintain.

##### Summary

SOLID principles are fundamental to good software design. They improve readability, maintainability, and flexibility, making your life easier as you develop and test your code. In the next post, we'll discuss Dependency Injection, another essential concept in TDD.


