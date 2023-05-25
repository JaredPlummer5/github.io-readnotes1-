# CRUD Operations

The HTTP method typically used to update a record through an API is the PUT method. This method is designed to replace the entire resource (record) with the new content provided in the request.

Example code snippet for updating a record using the PUT method in a server (Node.js with Express):

```javascript
// Server-side code
const express = require('express');
const app = express();

// Update a record
app.put('/api/records/:id', (req, res) => {
  const id = req.params.id;
  // Perform update operation based on the provided ID
  // ...
  res.send('Record updated successfully');
});

app.listen(3000, () => {
  console.log('Server listening on port 3000');
});
```

Example code snippet for updating a record using the PUT method in a React frontend (using `fetch` API):

```javascript
// Client-side code (React)
const updateRecord = (id, newData) => {
  fetch(`/api/records/${id}`, {
    method: 'PUT',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(newData),
  })
    .then(response => response.text())
    .then(data => {
      console.log(data); // Success message from the server
      // Handle success
      // ...
    })
    .catch(error => {
      console.error('Error:', error);
      // Handle error
      // ...
    });
};

// Example usage
const recordId = 123;
const updatedData = { /* New data to update the record */ };
updateRecord(recordId, updatedData);
```

REST methods that require an ID parameter are typically used for operations on specific resources. The methods that require an ID parameter are:

1. GET: Retrieve a specific resource by its ID.
2. PUT: Update a specific resource by its ID.
3. DELETE: Delete a specific resource by its ID.

These methods require the ID parameter to identify the resource on which the operation should be performed.

## Relationship between REST and CRUD

REST (Representational State Transfer) is an architectural style that provides guidelines for building networked applications. It defines a set of principles and constraints for designing web services. CRUD, on the other hand, represents the four basic functions (Create, Read, Update, Delete) that can be performed on data in a persistent storage system. CRUD operations align with the basic operations provided by RESTful APIs. In other words, CRUD operations are often used to implement the functionalities of a RESTful API. RESTful APIs use HTTP methods to map to CRUD operations (e.g., POST for create, GET for read, PUT for update, DELETE for delete).

Process of creating a RESTful API in 5 steps:

1. Define the Resources: Identify the resources your API will expose. These can be objects, entities, or data types that your API will interact with.

2. Design the URL Structure: Establish a consistent and meaningful URL structure that reflects the resources and their relationships. Each URL should represent a specific resource or a collection of resources.

3. Choose HTTP Methods: Determine which HTTP methods (GET, POST, PUT, DELETE, etc.) will be used for each API endpoint to perform the desired CRUD operations on the resources.

4. Implement Endpoint Handlers: Create the server-side logic to handle the API endpoints. Each endpoint should handle the corresponding HTTP method and perform the necessary CRUD operations on the resources.

5. Document and Test the API: Document the API endpoints, their functionality, and any required parameters or request/response formats. Additionally, thoroughly test the API endpoints using tools like Postman or automated tests to ensure they work as expected.

Example code snippets for each method in a server (Node.js with Express):

```javascript
// Server-side code
const express = require('express');
const app = express();

// Create a record
app.post('/api/records', (req, res) => {
  // Perform create operation
  // ...
  res.send('Record created successfully');
});

// Read a record or collection of records
app.get('/api/records', (req, res) => {
  // Perform read operation
  // ...
  res.send('Records retrieved successfully');
});

// Update a record
app.put('/api/records/:id', (req, res) => {
  const id = req.params.id;
  // Perform update operation based on the provided ID
  // ...
  res.send('Record updated successfully');
});

// Delete a record
app.delete('/api/records/:id', (req, res) => {
  const id = req.params.id;
  // Perform delete operation based on the provided ID
  // ...
  res.send('Record deleted successfully');
});

app.listen(3000, () => {
  console.log('Server listening on port 3000');
});
```

Example code snippets for each method in a React frontend (using `fetch` API):

```javascript
// Server-side code
//The first line imports the Express framework, which is a popular web application framework for Node.js.
//The second line imports the Mongoose library, which provides an elegant way to interact with MongoDB from Node.js.
//The third line initializes an Express application by invoking the express() function and assigns it to the app constant.

const express = require('express');
const mongoose = require('mongoose');
const app = express();

// Connect to MongoDB
//This code establishes a connection to the MongoDB database named "moviesdb" running locally on the default MongoDB port (27017).
//The connect() method of the Mongoose library is used to establish the connection. It takes in the MongoDB connection string as the first argument and an object of connection options as the second argument.
//If the connection is successful, the promise's then() callback is executed and logs a success message to the console. Otherwise, if there is an error connecting to the database, the catch() callback logs an error message.
mongoose.connect('mongodb://localhost/moviesdb', { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => {
    console.log('Connected to MongoDB');
  })
  .catch(error => {
    console.error('Error connecting to MongoDB:', error);
  });

// Define the movie schema
// This code defines the schema for the movie collection in the MongoDB database.
// The mongoose.Schema() constructor is used to create a new schema object.
// Inside the schema definition, each field (e.g., title, genre, director) is defined along with its data type (in this case, all fields are of type String).

const movieSchema = new mongoose.Schema({
  title: String,
  genre: String,
  director: String,
});

// Create the movie model
// This code creates a Mongoose model for the movie collection based on the movieSchema.
// The mongoose.model() method is used to create the model. It takes two arguments: the name of the model ('Movie' in this case) and the schema object (movieSchema).
const Movie = mongoose.model('Movie', movieSchema);

// Create a movie record
    // This code sets up a route for creating a movie record. It listens for a POST request to the /api/movies endpoint.
app.post('/api/movies', (req, res) => {
    // When a POST request is received, the provided movie data is extracted from the request body (req.body) and stored in the movieData variable.
    const movieData = req.body;
  // Create a new movie record in the MongoDB collection
  Movie.create(movieData)
    // The Movie.create() method is used to create a new movie record in the MongoDB database based on the movieData.
    .then(() => {
        // If the record creation is successful, the promise's then() callback sends a success response to the client with the message 'Movie created successfully'. Otherwise, if there is an error, the catch() callback logs an error message and sends a 500 status code with the message 'Error creating movie' as the response.
      res.send('Movie created successfully');
    })
    .catch(error => {
      console.error('Error creating movie:', error);
      res.status(500).send('Error creating movie');
    });
});

// Read movie records
app.get('/api/movies', (req, res) => {
  // Retrieve all movies from the MongoDB collection
  Movie.find()
    .then(movies => {
      res.send(movies);
    })
    .catch(error => {
      console.error('Error retrieving movies:', error);
      res.status(500).send('Error retrieving movies');
    });
});

// Update a movie record
If the update is successful, the promise's then() callback sends a success response to the client with the message 'Movie updated successfully'. If there is an error, the catch() callback logs an error message and sends a 500 status code with the message 'Error updating movie' as the response.
app.put('/api/movies/:id', (req, res) => {
    // This code sets up a route for updating a movie record. It listens for a PUT request to the /api/movies/:id endpoint, where :id represents the movie's unique identifier.
  const id = req.params.id;
    // When a PUT request is received, the movie ID is extracted from the request parameters (req.params.id) and stored in the id variable.
  const updatedData = req.body;
  // Find the movie by ID and update it in the MongoDB collection
  Movie.findByIdAndUpdate(id, updatedData)
    //The updated movie data is retrieved from the request body (req.body) and stored in the updatedData variable.
    //The Movie.findByIdAndUpdate() method is used to find the movie by its ID and update it with the new data in the MongoDB collection.
    .then(() => {
      res.send('Movie updated successfully');
    })
    .catch(error => {
      console.error('Error updating movie:', error);
      res.status(500).send('Error updating movie');
    });
});

// Delete a movie record
app.delete('/api/movies/:id', (req, res) => {
    //This code sets up a route for deleting a movie record. It listens for a DELETE request to the /api/movies/:id endpoint, where :id represents the movie's unique identifier.
  const id = req.params.id;
  // Find the movie by ID and remove it from the MongoDB collection
    //When a DELETE request is received, the movie ID is extracted from the request parameters (req.params.id) and stored in the id variable.
  Movie.findByIdAndRemove(id)
    //The Movie.findByIdAndRemove() method is used to find the movie by its ID and remove it from the MongoDB collection.
    .then(() => {
        //If the deletion is successful, the promise's then() callback sends a success response to the client with the message 'Movie deleted successfully'. 
        res.send('Movie deleted successfully');
    })
    .catch(error => {
        //If there is an error, the catch() callback logs an error message and sends a 500 status code with the message 'Error deleting movie' as the response.
      console.error('Error deleting movie:', error);
      res.status(500).send('Error deleting movie');
    });
});

app.listen(3000, () => {
  console.log('Server listening on port 3000');
});
```


