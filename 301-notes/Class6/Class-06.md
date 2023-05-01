# REST

REST stands for Representational State Transfer, and it is an architectural style used for designing networked applications. REST is commonly used in web services development to create scalable and interoperable systems.

At its core, REST is based on a set of principles that enable communication between clients and servers over HTTP (Hypertext Transfer Protocol). Here are the key principles of REST:

`Client-Server Architecture`: REST separates the client and server components, allowing them to evolve independently. The client is responsible for the user interface and user experience, while the server handles the business logic and data storage.

`Stateless Communication`: Each request from a client to a server must contain all the necessary information for the server to understand and process the request. The server does not maintain any client-specific state between requests. This approach allows for better scalability and fault tolerance.

`Uniform Interface`: REST emphasizes a uniform and standardized set of interactions between the client and server. This includes the use of standard HTTP methods (GET, POST, PUT, DELETE) to perform operations on resources, the use of URIs (Uniform Resource Identifiers) to identify resources, and the use of hypermedia (e.g., links) to navigate between resources.

`Resource-Based`: In REST, everything is treated as a resource, which can be a physical or logical entity. Resources are identified by unique URIs, and clients interact with these resources using standard HTTP methods.

`Representation-oriented`: Resources in REST are represented using different formats such as XML (eXtensible Markup Language) or JSON (JavaScript Object Notation). The server sends representations of resources to the client, and the client can manipulate and modify those representations before sending them back to the server.

`State Transfer`: REST is focused on the transfer of resource state between client and server. The server transfers the current state of a resource to the client, and the client can perform operations on that state, such as updating or deleting it.

By following these principles, RESTful systems can be built to be scalable, flexible, and easily accessible over the web. It has become a popular choice for designing APIs (Application Programming Interfaces) that allow different software systems to communicate and exchange data efficiently.

## Why don’t the techniques that we use in this class work well when we need to be able to talk to all of the machines in the world?

The techniques we use in this class (referring to traditional methods of computer communication) don't work well when we need to be able to talk to all of the machines in the world because they weren't designed with that scalability in mind. These techniques were built for communication within small, specific groups of machines, and they lack the flexibility and universality required for global communication.

## What is the HTTP protocol that Fielding and his friends created?

The HTTP protocol that Fielding and his friends created stands for Hypertext Transfer Protocol. It is the protocol used for communication between web browsers and web servers. HTTP defines the rules and conventions for requesting and transmitting data over the internet.

## GET

A GET request is an HTTP method used to retrieve a representation of a resource from a server. When a client (such as a web browser) sends a GET request to a server, it is asking for the server to return the specified resource, such as a web page, image, or file.

## POST

A POST request is an HTTP method used to submit data to be processed by the server. It is commonly used when submitting form data or creating a new resource on the server. The data sent in the body of the request is typically used to update or add new information on the server.

## PUT

PUT is an HTTP method used to update or replace an existing resource on the server. It sends the entire representation of the resource that needs to be updated or replaced. In other words, PUT is used to store or update a resource at a specific URL.

## PATCH

PATCH is an HTTP method used to partially update an existing resource on the server. It is similar to the PUT method, but instead of sending the entire representation of the resource, it only sends the specific changes or updates that need to be applied. PATCH is used when you want to modify certain fields or attributes of a resource without sending the entire representation.
