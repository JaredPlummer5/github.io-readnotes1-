# CRUD

- 100's = They're like your friend saying, "Hang on, I'm thinking." These are informational status codes. The server is saying it received your request, and it's processing it.

- 200's = These are like getting a high-five. They indicate success! The server understood your request, accepted it, and sent what you asked for.

- 300's = Imagine you're looking for your friend on the playground, but they moved to another spot. This is what these codes are like - redirection. The information you asked for is somewhere else, and the server is telling you where to look.

- 400's = These are like when you ask something silly or wrong, and your friend says, "Huh? That doesn't make sense." These codes mean there was a mistake in your request. It could be you asked for something that doesn't exist or in a way the server doesn't understand.

- 500's = Imagine your friend had a chance to respond, but they tripped and fell. These codes are like that. They indicate there's something wrong on the server's end, not yours.

Now, let's talk about specific codes:

- 202 = This is like your friend saying, "Got it, I'm on it!" The server has accepted your request but is still working on getting it done. So, you don't have a result yet, but it's coming.

- 308 = This is like your friend saying, "We moved the game to the other side of the playground. Go there!" It means the resource you're looking for has moved permanently, and you should go to the new location from now on.

If an update didn't return data to a client, a 204 No Content response would be fitting. It's like saying, "I did what you asked, but there's nothing to show you."

If a resource used to exist but no longer does, you'd use a 410 Gone status code. It's like saying, "Sorry, that thing you're looking for isn't here anymore."

The "Forbidden" status code is 403. It's like your friend saying, "Sorry, I can't let you do that." You asked for something, but the server won't give it to you, maybe because you don't have permission.

1. **Why do we need to pull our MongoDB database string out of our server and put it into our .env?**
    The MongoDB connection string often contains sensitive information like usernames, passwords, and server addresses. Putting this in a .env file and not including that file in version control (like git) helps protect these credentials. It also makes it easier to change the connection string based on the environment (development, production, etc.), without needing to modify the code.

2. **What is middleware?**
    Middleware is like a bridge that connects different components of an application. In Express.js, middleware functions have access to the request object, the response object, and the next middleware function in the application’s request-response cycle. They can execute any code, modify the request and response objects, end the request-response cycle, or call the next middleware function. 

3. **What does app.use(express.json()) do?**
    `app.use(express.json())` is a built-in middleware function in Express. It parses incoming requests with JSON payloads and is based on body-parser. This allows you to access `req.body` and the JSON contents of the request in your route handlers.

4. **What does the /:id mean in a route?**
    `/:id` in a route is a way of capturing a value from the URL. The value is accessible in the route handler as `req.params.id`. This is often used for routes that need to deal with a specific item in a database, identified by its id.

5. **What is the difference between PUT and PATCH?**
    PUT and PATCH are both HTTP methods and are used to update a resource. The main difference is that PUT updates the entire resource with the provided data, while PATCH only updates the fields that were provided in the data. This makes PATCH more efficient for updating a small number of fields.

6. **How do you make a default value in a schema?**
    In a Mongoose schema, you can provide a `default` value for a field as follows:
    ```javascript
    const bookSchema = new Schema({
      title: { type: String, default: 'Untitled' },
      // other fields...
    });
    ```
    In this example, if a new book is created without a title, 'Untitled' will be used.

7. **What does a 500 error status code mean?**
    A 500 status code is a generic "Internal Server Error" message, meaning something has gone wrong on the server, but the server can't be more specific on what the exact problem is.

8. **What is the difference between a status 200 and a status 201?**
    Both 200 and 201 are HTTP success status codes. 200 means "OK" and is a generic success status code, indicating that the request has succeeded. 201 means "Created" and is used to indicate that a request to create a new resource was successful.
