# ASP.NET Core web API documentation with Swagger / OpenAPI

## Introduction

- Swagger (OpenAPI) is a specification for describing REST APIs.
- It helps in minimizing work needed to connect decoupled services and reduces time for accurate documentation.
- Two main OpenAPI implementations for .NET are [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle.AspNetCore) and [NSwag](https://github.com/RicoSuter/NSwag).

## OpenAPI vs. Swagger

- OpenAPI is a specification.
- Swagger is tooling that uses the OpenAPI specification, including products like OpenAPIGenerator and SwaggerUI.

## OpenAPI Specification (`openapi.json`)

- Describes the capabilities of the API based on XML and attribute annotations.
- Drives tooling such as SwaggerUI.
- Example of an OpenAPI specification:

```json
{
  "openapi": "3.0.1",
  "info": {
    "title": "API V1",
    "version": "v1"
  },
  "paths": {
    "/api/Todo": {
      "get": {
        "tags": ["Todo"],
        "operationId": "ApiTodoGet",
        "responses": {
          "200": {
            "description": "Success",
            "content": {
              "text/plain": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/ToDoItem"
                  }
                }
              },
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/ToDoItem"
                  }
                }
              },
              "text/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/ToDoItem"
                  }
                }
              }
            }
          }
        }
      },
      "post": {...},
      "/api/Todo/{id}": {
        "get": {...},
        "put": {...},
        "delete": {...}
      }
    }
  },
  "components": {
    "schemas": {
      "ToDoItem": {
        "type": "object",
        "properties": {
          "id": {
            "type": "integer",
            "format": "int32"
          },
          "name": {
            "type": "string",
            "nullable": true
          },
          "isCompleted": {
            "type": "boolean"
          }
        },
        "additionalProperties": false
      }
    }
  }
}
```

#### Swagger UI

- [Swagger UI](https://swagger.io/swagger-ui/) offers a web-based UI that provides information about the service using the generated OpenAPI specification.
- It can be hosted in ASP.NET Core app using a middleware registration call.
- Allows testing of public action methods in controllers.
- ![Swagger UI Example](https://learn.microsoft.com/en-us/aspnet/core/tutorials/web-api-help-pages-using-swagger/_static/swagger-ui.png%3Fview%3Daspnetcore-2.1)


## Conclusion

- The article provides an overview of using Swagger and OpenAPI with ASP.NET Core, including creating specifications, using Swagger UI, and understanding the difference between OpenAPI and Swagger.
- It serves as a guide for developers to create and manage API documentation effectively.

(Note: The content has been processed for brevity, and this summary includes the main points and code snippets from the article.)

## Creating Unit Tests for ASP.NET MVC Applications (C#)

### Summary

Learn how to create unit tests for controller actions in ASP.NET MVC applications. The tutorial covers testing the view, view data, and action result returned by a controller.

### Creating the Controller under Test

- **ProductController** with two action methods: `Index()` and `Details(int Id)`.

```csharp
namespace Store.Controllers
{
     public class ProductController : Controller
     {
          public ActionResult Index()
          {
               throw new NotImplementedException();
          }

          public ActionResult Details(int Id)
          {
               return View("Details");
          }
     }
}
```

### Testing the View returned by a Controller

- Test whether the `ProductController.Details()` action returns the "Details" view.

```csharp
namespace StoreTests.Controllers
{
     [TestClass]
     public class ProductControllerTest
     {
          [TestMethod]
          public void TestDetailsView()
          {
               var controller = new ProductController();
               var result = controller.Details(2) as ViewResult;
               Assert.AreEqual("Details", result.ViewName);
          }
     }
}
```

### Testing the View Data returned by a Controller

- Test whether the `Details()` action returns the correct product.

```csharp
namespace StoreTests.Controllers
{
     [TestClass]
     public class ProductControllerTest
     {
          [TestMethod]
          public void TestDetailsViewData()
          {
               var controller = new ProductController();
               var result = controller.Details(2) as ViewResult;
               var product = (Product) result.ViewData.Model;
               Assert.AreEqual("Laptop", product.Name);
          }
     }
}
```

### Testing the Action Result returned by a Controller

- Test whether the `Details()` action returns the correct action result based on the product Id.

```csharp
namespace StoreTests.Controllers
{
     [TestClass]
     public class ProductControllerTest
     {
          [TestMethod]
          public void TestDetailsRedirect()
          {
               var controller = new ProductController();
               var result = (RedirectToRouteResult) controller.Details(-1);
               Assert.AreEqual("Index", result.Values["action"]);
          }
     }
}
```

### Conclusion

The tutorial provides a comprehensive guide to building unit tests for MVC controller actions, including verifying the right view, checking the contents of View Data, and testing different types of action results.

Certainly! Here are the markdown notes and code snippets from the page on testing controller logic in ASP.NET Core:

## Unit Test Controller Logic in ASP.NET Core

### Introduction

- Unit tests involve testing a part of an app in isolation from its infrastructure and dependencies.
- When unit testing controller logic, only the contents of a single action are tested, not the behavior of its dependencies or the framework itself.

### Unit Testing Controllers

- Set up unit tests of controller actions to focus on the controller's behavior.
- A controller unit test avoids scenarios such as filters, routing, and model binding.
- Tests that cover the interactions among components that collectively respond to a request are handled by integration tests.

### Example Controller

```csharp
public class HomeController : Controller
{
    private readonly IBrainstormSessionRepository _sessionRepository;

    public HomeController(IBrainstormSessionRepository sessionRepository)
    {
        _sessionRepository = sessionRepository;
    }

    public async Task<IActionResult> Index()
    {
        var sessionList = await _sessionRepository.ListAsync();
        var model = sessionList.Select(session => new StormSessionViewModel()
        {
            Id = session.Id,
            DateCreated = session.DateCreated,
            Name = session.Name,
            IdeaCount = session.Ideas.Count
        });

        return View(model);
    }

    public class NewSessionModel
    {
        [Required]
        public string SessionName { get; set; }
    }

    [HttpPost]
    public async Task<IActionResult> Index(NewSessionModel model)
    {
        if (!ModelState.IsValid)
        {
            return BadRequest(ModelState);
        }
        else
        {
            await _sessionRepository.AddAsync(new BrainstormSession()
            {
                DateCreated = DateTimeOffset.Now,
                Name = model.SessionName
            });
        }

        return RedirectToAction(actionName: nameof(Index));
    }
}
```

### Testing the GET Index Method

```csharp
[Fact]
public async Task Index_ReturnsAViewResult_WithAListOfBrainstormSessions()
{
    // Arrange
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    mockRepo.Setup(repo => repo.ListAsync())
        .ReturnsAsync(GetTestSessions());
    var controller = new HomeController(mockRepo.Object);

    // Act
    var result = await controller.Index();

    // Assert
    var viewResult = Assert.IsType<ViewResult>(result);
    var model = Assert.IsAssignableFrom<IEnumerable<StormSessionViewModel>>(
        viewResult.ViewData.Model);
    Assert.Equal(2, model.Count());
}
```

### Testing the POST Index Method

```csharp
[Fact]
public async Task IndexPost_ReturnsBadRequestResult_WhenModelStateIsInvalid()
{
    // Arrange
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    mockRepo.Setup(repo => repo.ListAsync())
        .ReturnsAsync(GetTestSessions());
    var controller = new HomeController(mockRepo.Object);
    controller.ModelState.AddModelError("SessionName", "Required");
    var newSession = new HomeController.NewSessionModel();

    // Act
    var result = await controller.Index(newSession);

    // Assert
    var badRequestResult = Assert.IsType<BadRequestObjectResult>(result);
    Assert.IsType<SerializableError>(badRequestResult.Value);
}

[Fact]
public async Task IndexPost_ReturnsARedirectAndAddsSession_WhenModelStateIsValid()
{
    // Arrange
    var mockRepo = new Mock<IBrainstormSessionRepository>();
    mockRepo.Setup(repo => repo.AddAsync(It.IsAny<BrainstormSession>()))
        .Returns(Task.CompletedTask)
        .Verifiable();
    var controller = new HomeController(mockRepo.Object);
    var newSession = new HomeController.NewSessionModel()
    {
        SessionName = "Test Name"
    };

    // Act
    var result = await controller.Index(newSession);

    // Assert
    var redirectToActionResult = Assert.IsType<RedirectToActionResult>(result);
    Assert.Null(redirectToActionResult.ControllerName);
    Assert.Equal("Index", redirectToActionResult.ActionName);
    mockRepo.Verify();
}
```


