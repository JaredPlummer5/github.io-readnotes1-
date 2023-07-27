# ASP.NET MVC Routing Overview (C#)

## What is Routing?

Routing is the system in ASP.NET MVC that decides what happens when a user enters a URL into their web browser. Think of it like a postman delivering mail. The postman uses an address to decide where to deliver the mail. In the same way, routing uses the URL to decide where to send the request.

## Using the Default Route Table

When you create a new ASP.NET MVC application, routing is set up for you automatically. It is set up in two places: 

1. **Web.config file:** This is the configuration file for your application. It contains settings that ASP.NET uses to manage your application. Imagine it as the rules you might see posted on a classroom wall.

```xml
<system.web>
    <httpModules>
        <!-- Routing Module -->
    </httpModules>
    <httpHandlers>
        <!-- Routing Handler -->
    </httpHandlers>
</system.web>
<system.webServer>
    <modules>
        <!-- Routing Module -->
    </modules>
    <handlers>
        <!-- Routing Handler -->
    </handlers>
</system.webServer>
```

2. **Global.asax file:** This file contains event handlers for application lifecycle events. This is like the school bell that rings at the start and end of the school day.

Here's a simple example of what the `Global.asax` file might look like.

```csharp
public class MvcApplication : System.Web.HttpApplication
{
    public static void RegisterRoutes(RouteCollection routes)
    {
        routes.IgnoreRoute("{resource}.axd/{*pathInfo}");

        routes.MapRoute(
            "Default",                                              // Route name
            "{controller}/{action}/{id}",                           // URL with parameters
            new { controller = "Home", action = "Index", id = "" }  // Parameter defaults
        );
    }

    protected void Application_Start()
    {
        RegisterRoutes(RouteTable.Routes);
    }
}
```

In this example, a route named "Default" is created. The URL format for this route is `{controller}/{action}/{id}`. This is like a template that the postman uses to understand the address.

## How the Default Route Works

Let's say you enter the following URL in your browser:

```
/Home/Index/3
```

The "Default" route will break this down into three parts:

- controller = "Home"
- action = "Index"
- id = 3

This is like the postman breaking down the address into street, house number, and apartment number. The routing system will then try to find a "Home" controller, an "Index" action within that controller, and pass "3" as the id.

The following code is then executed:

```csharp
HomeController.Index(3)
```

This calls the `Index` method on the `HomeController`, passing `3` as the `id`.

## Routing With Different Controller Methods

Different controller actions can handle different URLs. Here are some examples:

1. An `Index` action that takes a `string` parameter called `id`. A URL like `/Home` will call this action with an empty `id`.

```csharp
public class HomeController : Controller
{
    public ActionResult Index(string id)
    {
        return View();
    }
}
```

2. An `Index` action that takes no parameters. The URL `/Home` or `/Home/Index/3` will call this action (the `id` is ignored).

```csharp
public class HomeController : Controller
{
    public ActionResult Index()
    {
        return View();
    }
}
```

3. An `Index` action with an optional `id` parameter. The URL `/Home` will call this action without an `id`.

```csharp
public class HomeController : Controller
{
    public ActionResult Index(int? id)
    {
        return View();
    }
}
```

4. An `Index` action with a required `id` parameter. The URL `/Home` will fail to call this action because it expects an `id`. But `/Home/Index/3` works just fine because it includes an `id`.

```csharp
public class HomeController : Controller
{
    public ActionResult Index(int id)
    {
        return View();
    }
}
```

In conclusion, routing is a very important part of ASP.NET MVC. It determines how URLs map to controller actions, which is key to how users interact with your application. Just like the postman uses addresses to deliver mail, ASP.NET uses routes to deliver requests.

# Routing in ASP.NET Core

## What is Routing?

Let's imagine you are in a huge library with millions of books. How do you find the book you want? You'll need a system that can guide you directly to the book, right? This system could be like "Go to the 3rd aisle, then to the 2nd shelf from the top, and pick the 5th book from the left". That's pretty much what Routing does in ASP.NET Core.

Routing is a system in ASP.NET Core that decides what code should run when a user visits a particular URL. It takes incoming requests and maps them to specific controller actions.

## Basics of Routing in ASP.NET Core

Let's start with a simple example of how routing works in an ASP.NET Core application. When you create a new ASP.NET Core MVC project, a `Startup.cs` file is created which includes a method named `Configure()`. This method sets up the pipeline of middleware for your application. Middleware are like the different sections of our library, each having its specific task.

In the `Configure()` method, you can see a line that adds MVC to the middleware pipeline and enables the default route.

```csharp
app.UseEndpoints(endpoints =>
{
    endpoints.MapControllerRoute(
        name: "default",
        pattern: "{controller=Home}/{action=Index}/{id?}");
});
```

Here, the `MapControllerRoute()` method is setting up the default route. The pattern of the route is "{controller=Home}/{action=Index}/{id?}". This can be broken down into three segments:

- Controller: The first part of the URL, defaults to "Home"
- Action: The second part of the URL, defaults to "Index"
- Id: The third part of the URL, it's optional

For example, if we go to the URL "/Books/Details/5", the "Books" maps to the BooksController, "Details" maps to an action method named Details inside BooksController, and "5" will be passed as an argument to the Details action method. 

## Attribute Routing

In ASP.NET Core, we also have something called attribute routing. This is like having a GPS in our library that directly guides us to our book. You can set routes directly on the controllers and actions.

Here's an example of attribute routing in a controller:

```csharp
[Route("api/[controller]")]
public class BooksController : Controller
{
    // This action can be reached at "/api/books/all"
    [HttpGet("all")]
    public IActionResult GetAllBooks()
    {
        // Code to get all books
    }

    // This action can be reached at "/api/books/5"
    [HttpGet("{id}")]
    public IActionResult GetBook(int id)
    {
        // Code to get the book with id = 5
    }
}
```

In this example, the `[Route("api/[controller]")]` attribute sets the base route for this controller to "/api/books". Then, each action has its own `[HttpGet()]` attribute that further specifies its route.

## Conclusion

So, routing in ASP.NET Core is a little bit like having a librarian guide us directly to our book. It helps us match the right code with the URL entered by the user. It gives us a way to organize our code and helps users find what they're looking for in our application. It's an important part of how users interact with our app.

# Routing in ASP.NET Core

Routing is like a GPS system for an application. It helps your application understand which part to run when a specific URL is requested.

## Comparing a Terminal Middleware and Routing

A middleware is like a checkpost in a highway. When a request comes in, it can decide to handle it, or pass it to the next checkpost. A terminal middleware is like the last checkpost that handles the request if no previous checkpost did.

On the other hand, routing checks the URL of the request and decides which part of the application to run. It's like a traffic cop directing cars based on their destination.

## URL Matching

This is how routing decides which part of the application to run based on the URL. It's like how you'd find a page in a book based on the page number.

## Route Template Precedence and Endpoint Selection Order

Sometimes, more than one route could match a URL. Route template precedence and endpoint selection order decide which one to use. It's like if you're at a fork in the road, and your GPS has to choose one path.

## URL Generation Concepts

This is the opposite of URL matching. It's about generating a URL based on which part of the application to run. It's like finding the address of a house based on the house itself.

## Middleware Code Snippet Example

Here's an example of middleware:

```csharp
app.Use(async (context, next) =>
{
    // Do something before the next middleware
    await next.Invoke();
    // Do something after the next middleware
});
```

In this code, `context` is the request, and `next` is the next middleware. The code above it runs before the next middleware, and the code below it runs after.

## Route Template Reference

A route template is like a pattern that the routing system uses to match URLs. Here's an example:

```
"{controller=Home}/{action=Index}/{id?}"
```

This matches URLs like `/Home/Index/3` and breaks it down into parts: `controller = "Home"`, `action = "Index"`, and `id = 3`.

## Complex Segments

Sometimes, a segment (part of the URL) might be complex and contain multiple parts. For example:

```
"blog/{*slug}"
```

In this case, `slug` could be something like `2020/12/my-first-post`.

## Route Constraint Reference

Constraints are like rules that a segment must follow to match a route. For example:

```
"{id:int}"
```

In this case, `id` must be an integer.

## Regular Expressions in Constraints

You can also use regular expressions in constraints, which are like more powerful rules. For example:

```
"{id:regex(\\d+)}"
```

This also requires `id` to be an integer.


## URL Generation Reference

Here are some concepts related to URL generation:

- Addresses: These are like templates for URLs that you can fill in.
- Ambient values and explicit values: These are values that are already available vs. values that you provide.
- URL generation process: This is the process of creating a URL from an address and some values.
