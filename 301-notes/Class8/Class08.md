# APIs

## What does REST stand for?

REST stands for Representational State Transfer.

- REST is important because it provides a standardized way of building web APIs that are scalable, flexible, and easy to understand. Some of the key benefits of using REST include:

- Scalability: RESTful APIs can handle large amounts of traffic and scale easily as the user base grows.

- Interoperability: RESTful APIs are based on standardized HTTP methods and formats, which makes it easy to integrate with other systems and technologies.

- Flexibility: RESTful APIs allow clients to access and manipulate resources in a variety of formats, such as JSON or XML, depending on their needs.

Simplified client-server interactions: RESTful APIs use a stateless architecture, which means that each request contains all the information needed for the server to fulfill it. This makes it easy to cache responses and simplify the overall architecture.

Easy to understand: RESTful APIs are based on simple, well-defined principles that make it easy for developers to understand and use them.

## REST APIs are designed around a resource

In REST, resources are the key building blocks that the API is designed around. Think of a resource as something that the API can provide access to, such as a user account, a product listing, or a blog post.

When you interact with a REST API, you are typically performing operations on these resources, such as retrieving information about a user account, updating a product listing, or creating a new blog post. Each of these operations corresponds to an HTTP method, such as GET, POST, or PUT, that is used to interact with the API.

For example, if you wanted to retrieve information about a user account from a REST API, you would typically send a GET request to a specific URL that corresponds to that resource. The API would then respond with the information about that resource in a format such as JSON or XML.

The key idea behind this design is that resources are self-contained and can be accessed and manipulated in a standardized way. This makes it easy for clients, such as web applications or mobile apps, to interact with the API and perform operations on the resources in a consistent way.

Overall, the resource-based design of REST APIs provides a simple and standardized way of building web APIs that are easy to understand and use, even for non-technical users.

Example:

```

const express = require('express');
const app = express();

// Define a resource - in this case, a list of books
const books = [
  { id: 1, title: 'The Hitchhiker\'s Guide to the Galaxy', author: 'Douglas Adams' },
  { id: 2, title: 'To Kill a Mockingbird', author: 'Harper Lee' },
  { id: 3, title: '1984', author: 'George Orwell' }
];

// Define a route to retrieve all books
app.get('/books', (req, res) => {
  res.json(books);
});

// Define a route to retrieve a specific book by ID
app.get('/books/:id', (req, res) => {
  const id = req.params.id;
  const book = books.find(book => book.id == id);
  if (book) {
    res.json(book);
  } else {
    res.status(404).json({ error: 'Book not found' });
  }
});

// Define a route to add a new book
app.post('/books', (req, res) => {
  const newBook = req.body;
  books.push(newBook);
  res.json(newBook);
});

// Define a route to update an existing book by ID
app.put('/books/:id', (req, res) => {
  const id = req.params.id;
  const book = books.find(book => book.id == id);
  if (book) {
    book.title = req.body.title;
    book.author = req.body.author;
    res.json(book);
  } else {
    res.status(404).json({ error: 'Book not found' });
  }
});

// Define a route to delete an existing book by ID
app.delete('/books/:id', (req, res) => {
  const id = req.params.id;
  const bookIndex = books.findIndex(book => book.id == id);
  if (bookIndex !== -1) {
    books.splice(bookIndex, 1);
    res.json({ message: 'Book deleted successfully' });
  } else {
    res.status(404).json({ error: 'Book not found' });
  }
});

// Start the server
app.listen(3000, () => {
  console.log('Server started on port 3000');
});


```

In this example, we define a resource as a list of books, with each book represented as an object with an ID, title, and author. We then define routes for each HTTP method (`GET`, `POST`, `PUT`, and `DELETE`) that allow clients to retrieve, create, update, and delete books.

For example, to retrieve all books, a client would send a GET request to the /books endpoint, which would respond with the list of books in JSON format. To retrieve a specific book by ID, the client would send a GET request to the /books/:id endpoint, where :id is the ID of the book to retrieve. And so on for the other methods.

This is just a simple example, but it illustrates how a REST API can be designed around resources and how each resource can be accessed and manipulated using HTTP methods.

## What is an identifier of a resource? Give an example

An identifier of a resource is a unique identifier that is used to distinguish one resource from another. Think of it like a name or a serial number that helps you identify something in the real world.

For example, let's say we have a REST API that provides access to a list of books. Each book in the list would be considered a resource, and we could use a unique identifier, such as an ISBN (International Standard Book Number), to identify each book.

An ISBN is a unique identifier assigned to each book by the publisher. It consists of 13 digits and is typically printed on the back cover of the book. For example, the ISBN for "To Kill a Mockingbird" by Harper Lee is 9780061120084.

In our REST API, we could use the ISBN as the identifier for each book resource. So if a client wants to retrieve information about a specific book, they could send a GET request to a URL that includes the ISBN as a parameter, like this:

`GET /books/9780061120084`

The server would then look up the book with that ISBN in the list of books and return its information in the response.

In this way, the ISBN serves as a unique identifier for each book resource, making it easy for clients to retrieve information about specific books and manipulate them in a standardized way.

## What are the most common HTTP verbs?

1. GET:

    - The GET method is used to retrieve a resource or a collection of resources from the server. It is a safe and idempotent method, which means that it can be called multiple times without changing the state of the server or the resource being retrieved.

    Example usage:

    `GET /books/123`

    This request retrieves the book with ID 123 from the server.

    Coding example:

    ```

    app.get('/books/:id', (req, res) => {
     const id = req.params.id;
    // Look up the book with the given ID in the database
    const book = db.find(book => book.id === id);
    if (book) {
      res.json(book);
    } else {
     res.status(404).send('Book not found');
    }
    });

    ```

2. POST

- The POST method is used to send data to the server to create a new resource. It is not idempotent, which means that calling it multiple times can create multiple resources.

Example usage:

    ```

    POST /books
    {
      "title": "The Hitchhiker's Guide to the Galaxy",
      "author": "Douglas Adams"
    }

    ```

    This request creates a new book resource with the given title and author on the server.

    Coding example:

    ```

    app.post('/books', (req, res) => {
      const newBook = req.body;
      // Add the new book to the database
      db.push(newBook);
      // Send a response with the newly created book and its ID
      res.status(201).json({ id: newBook.id, ...newBook });
    });

    ```

    3. PUT:

    - The PUT method is used to send data to the server to update an existing resource. It is idempotent, which means that calling it multiple times with the same data has the same effect as calling it once.

    Example usage:

    ```
    PUT /books/123
    {
    "title": "The Hitchhiker's Guide to the Galaxy",
    "author": "Douglas Adams"
    }


    ```
    This request updates the book with ID 123 on the server with the given title and author.

    Coding example:

```

    app.put('/books/:id', (req, res) => {
    const id = req.params.id;
    const updatedBook = req.body;
    // Look up the book with the given ID in the database
    const index = db.findIndex(book => book.id === id);
    if (index !== -1) {
    // Update the book with the given ID in the database
    db[index] = updatedBook;
    // Send a response with the updated book
    res.json(updatedBook);
    } else {
    res.status(404).send('Book not found');
    }
    });

```

    4. DELETE:

    - The DELETE method is used to delete a resource from the server. It is idempotent, which means that calling it multiple times has the same effect as calling it once.
    
    Example usage:

    `DELETE /books/123`

    This request deletes the book with ID 123 from the server.

    Coding example:

    ```
    app.delete('/books/:id', (req, res) => {
    const id = req.params.id;
    // Look up the book with the given ID in the database
    const index = db.findIndex(book => book.id === id);
    if (index !== -1) {
    // Remove the book with the given ID from the database
    db.splice(index, 1);
    // Send a response with a message indicating that the book was deleted
    res.send('Book deleted successfully');
    }
    })

    ```

## What should the URIs be based on?

URIs (Uniform Resource Identifiers) in a REST API should be based on the resources that the API provides access to.

The URI should identify the resource uniquely and should be hierarchical in nature. For example, consider a REST API that provides access to a collection of books. The URI for retrieving a specific book might look like this:

```
GET /books/123
```

In this example, `/books` identifies the collection of books, and `123` identifies the specific book within that collection.

The URI should also be designed in a way that is intuitive and easy to understand for developers who are using the API. It should use clear and meaningful names for resources and avoid unnecessary complexity.

Overall, the URI should be based on the resources that the API provides access to and should be designed in a way that makes it easy for clients to understand and use the API.

## Give an example of a good URI.

Here's an example of a good URI and an explanation of what it is doing:

```
GET /books/123/chapters/5
```

In this example, the URI is designed to retrieve a specific chapter (chapter 5) of a specific book (book 123) from a REST API that provides access to a collection of books.

Breaking down the URI:

- `GET`: This is the HTTP method that is being used to retrieve the resource.
- `/books`: This is the base URI that identifies the collection of books.
- `/123`: This is the unique identifier of the specific book that we want to retrieve a chapter from.
- `/chapters`: This is a sub-resource of the book that represents the collection of chapters in the book.
- `/5`: This is the unique identifier of the specific chapter that we want to retrieve.

The URI is hierarchical in nature and clearly identifies the resource that we want to retrieve (chapter 5 of book 123). It is also designed in a way that is intuitive and easy to understand, using clear and meaningful names for the resources.

Overall, this URI is a good example of how URIs in a REST API should be designed to provide easy and intuitive access to resources.

## What does it mean to have a ‘chatty’ web API? Is this a good or a bad thing?

A 'chatty' web API is one that requires multiple requests to be made to the server in order to perform a single task. This can happen when the API is designed with small, fine-grained resources that don't provide enough functionality in a single request.

For example, consider a REST API that provides access to a collection of books. If the API requires a separate request to be made for each chapter of a book, this would be considered a chatty API. In this case, retrieving all the chapters of a book would require multiple requests to the server, which can be slow and inefficient.

Having a chatty web API is generally considered a bad thing, as it can lead to slower performance and increased network traffic. It can also make the API more difficult to use and less intuitive for developers.

To avoid a chatty API, the API design should be based on meaningful resources that provide enough functionality in a single request to perform the task at hand. This can involve combining multiple resources into a single resource, or providing more functionality in a single resource.

Overall, it's important to strike a balance between providing enough functionality in a single request and keeping the resources meaningful and manageable.

## What status code does a successful GET request return?

A successful GET request should return a HTTP status code of 200 (OK) to indicate that the server successfully processed the request and is returning the requested data in the response body.

The 200 status code is part of the 2xx (Successful) status code range, which indicates that the request was successful and the server was able to fulfill the client's request.

Other status codes in the 2xx range that might be returned for a successful GET request include:

- 204 (No Content): This is used when the server successfully processed the request, but there is no content to return in the response body.

- 206 (Partial Content): This is used when the server is returning a partial representation of the resource, such as when requesting a specific range of bytes from a file.

In general, a successful GET request should return a 200 status code, unless there is a specific reason to return a different status code, such as when there is no content to return or when returning a partial representation of the resource.

Example:

Here's an example of a simple Express route handler that returns a 200 status code for a successful GET request:

```
app.get('/books/:id', (req, res) => {
  const bookId = req.params.id;
  
  // Retrieve the book with the given ID from the database
  const book = findBookById(bookId);
  
  if (book) {
    // Return the book in the response body with a 200 status code
    res.status(200).json(book);
  } else {
    // Return a 404 status code if the book with the given ID was not found
    res.status(404).send('Book not found');
  }
});
```

In this example, the route handler is registered for the `/books/:id` route using the `app.get()` method. When a GET request is made to this route with a valid book ID, the server retrieves the book from the database and returns it in the response body with a 200 status code using the `res.status(200).json()` method. If the book with the given ID is not found, the server returns a 404 status code using the `res.status(404).send()` method.

Note that this example assumes the `findBookById()` function returns the book with the given ID from the database.

## What status code does an unsuccessful GET request return?

An unsuccessful GET request can return different HTTP status codes depending on the specific reason for the failure. Some common status codes that might be returned for an unsuccessful GET request include:

- 404 (Not Found): This is used when the requested resource is not found on the server. For example, if the client requested a resource that doesn't exist or an invalid URL, the server would return a 404 status code.

- 400 (Bad Request): This is used when the request is invalid or cannot be processed by the server. For example, if the client sends invalid parameters in the request or the request is missing required parameters, the server would return a 400 status code.

- 401 (Unauthorized): This is used when the client is not authorized to access the requested resource. For example, if the client is not authenticated or does not have the necessary permissions to access the resource, the server would return a 401 status code.

- 403 (Forbidden): This is used when the server understands the request but refuses to fulfill it due to access restrictions. For example, if the client requests a resource that the server has restricted access to, the server would return a 403 status code.

- 500 (Internal Server Error): This is used when the server encounters an unexpected error while processing the request. For example, if there is a problem with the server configuration or the database, the server would return a 500 status code.

In general, an unsuccessful GET request should return a status code that accurately reflects the reason for the failure. This can help the client understand why the request failed and take appropriate action.


## What status code does a successful POST request return?

A successful `POST` request should return a HTTP status code of 201 (Created) to indicate that the server successfully created a new resource based on the request. The server should also include a `Location` header in the response to specify the URI of the newly created resource.

Here's an example of a simple Express route handler that returns a 201 status code for a successful `POST` request:

```
app.post('/books', (req, res) => {
  const newBook = req.body;
  
  // Add the new book to the database
  const book = addBook(newBook);
  
  // Return a 201 status code with the URI of the newly created resource in the Location header
  res.status(201).location(`/books/${book.id}`).json(book);
});
```

In this example, the route handler is registered for the `/books` route using the `app.post()` method. When a POST request is made to this route with the data for a new book in the request body, the server adds the new book to the database and returns a 201 status code with the URI of the newly created resource in the `Location` header using the `res.status(201).location().json()` methods.

Note that this example assumes the `addBook()` function adds the new book to the database and returns the book with a unique ID.

## What status code does a successful DELETE request return?

A successful `DELETE` request should return a HTTP status code of 204 (No Content) to indicate that the server successfully processed the request and deleted the resource.

Unlike other HTTP methods such as GET and POST, a `DELETE` request does not typically return a response body, since the resource being deleted no longer exists on the server. Instead, the server can simply return a 204 status code to indicate that the request was successfully processed and the resource was deleted.

Here's an example of a simple Express route handler that returns a 204 status code for a successful `DELETE` request:

```
app.delete('/books/:id', (req, res) => {
  const bookId = req.params.id;
  
  // Delete the book with the given ID from the database
  const deletedBook = deleteBookById(bookId);
  
  if (deletedBook) {
    // Return a 204 status code if the book was successfully deleted
    res.status(204).send();
  } else {
    // Return a 404 status code if the book with the given ID was not found
    res.status(404).send('Book not found');
  }
});
```

In this example, the route handler is registered for the `/books/:id` route using the `app.delete()` method. When a `DELETE` request is made to this route with a valid book ID, the server deletes the book from the database and returns a 204 status code using the `res.status(204).send()` method. If the book with the given ID is not found, the server returns a 404 status code using the `res.status(404).send()` method.
