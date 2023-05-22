# SQL, MongoDB and Mongoose

**1. What does SQL stand for?**
    
    SQL stands for "Structured Query Language". It's a programming language used to communicate with and manipulate databases.
    
    **2. What is a relational database?**
    
    A relational database is a type of database that organizes data into tables, and these tables (also called 'relations') can be linked to each other based on their common data. Each table consists of rows (records) and columns (fields).
    
    **3. What type of structure does a relational database work with?**
    
    A relational database works with a structured, table-based format. Each table has a fixed structure with a set number of columns (fields) that define the data to be stored, and each row in the table represents a single record.
    
    **4. What is a ‘schema’?**
    
    A schema in a database is like a blueprint. It defines how data is organized and how the relations among them are associated. It outlines how data is stored in the database in terms of tables, fields, relationships, constraints, and indexes.
    
    **5. What is a NoSQL database?**
    
    A NoSQL database is a type of database designed to handle data that doesn't fit well in a rigid, table-like structure that SQL databases use. They can handle unstructured data and can scale horizontally across servers.
    
    **6. How does it work?**
    
    NoSQL databases work by storing data in a format that is either key-value pairs, wide-column stores, a graph format or document-oriented. They don't require a fixed schema and can handle large volumes of data.
    
    **7. What is inside of a MongoDB database?**
    
    Inside a MongoDB database, data is stored in a format called BSON, which is similar to JSON. Data is organized into 'collections' (similar to tables in SQL), and each individual data point is a 'document' (similar to a row in SQL), which can contain various 'fields' (like columns in SQL). But unlike SQL, each document can have a different structure and different types of data.
    
    **8. Which is more flexible - SQL or MongoDB? And why?**
    
    MongoDB is generally more flexible than SQL. This is because MongoDB does not require a fixed schema, so data can be stored in various formats and structures. In contrast, SQL requires a predefined schema and the data must fit into this structure.
    
    **9. What is the disadvantage of a NoSQL database?**
    
    One disadvantage of NoSQL databases is that they lack the standardization that SQL databases have. This means different NoSQL databases can have different query languages and APIs, which can create a steeper learning curve.
    
    Also, while NoSQL databases can handle unstructured data and scale horizontally, they generally don't support complex queries and transactions as well as SQL databases do. This makes them less suitable for applications where data integrity and consistency is crucial.

## Five differences between SQL and NoSQL databases

### SQL

- SQL databases are primarily called as Relational Databases (RDBMS)

#### What is a Relational Databases

A relational database is a type of database that organizes data into tables, or "relations". These tables consist of rows and columns where each row represents a unique record, and each column represents a specific field within the record. The key idea is that these tables can be linked, or related, based on data they share, which is a key concept of the "relational" part.

SQL (Structured Query Language) is the standard language for dealing with relational databases. SQL can be used to insert, search, update, and delete database records. It can also be used to create and modify databases and tables. SQL is based on the relational algebra and tuple relational calculus.

Here are a few examples of SQL commands:

- SELECT: Extract data from a database.

- INSERT INTO: Insert new data into a database.

- UPDATE: Update data in a database.

- DELETE: Delete data from a database.

Let's consider a simple example. Suppose we have two tables: a "Customers" table and an "Orders" table. In the "Customers" table, we might have fields like CustomerID, Name, and Address. In the "Orders" table, we might have OrderID, Product, and CustomerID.

The "CustomerID" field in the "Customers" table is a primary key: it is unique to each customer. The "CustomerID" field in the "Orders" table is a foreign key: it refers to the CustomerID in the "Customers" table. This is the fundamental basis for a relationship in a relational database: you can use this common field to find all orders made by a particular customer.

This is a powerful concept, because it allows you to structure your data in a way that is intuitive and flexible. It also allows you to perform complex queries by joining tables together. In SQL, you could do this using the JOIN keyword. For example, to find the names of all customers who ordered a particular product, you could use a query like:

```sql

SELECT Customers.Name 

FROM Customers 

JOIN Orders ON Customers.CustomerID = Orders.CustomerID 

WHERE Orders.Product = 'Some Product';

```

Example:

Let's start by thinking about your toys. You have a box of toy cars, right? Each car might have its own color, size, brand, and type. You might also have a box of toy action figures. Each action figure might have a name, a costume, a superpower, and a team they belong to.

A relational database is a lot like these boxes of toys. In a relational database, each box of toys can be thought of as a 'table'. Each table is made up of different 'rows', just like how your box has different toys. Each toy (or row) has different properties (like color, size, brand, etc.), and these are called 'columns' in a database table.

So, if we create a table for your toy cars, it might look like this in SQL:

```sql
CREATE TABLE ToyCars (
    ID INT PRIMARY KEY,
    Color VARCHAR(20),
    Size VARCHAR(20),
    Brand VARCHAR(50),
    Type VARCHAR(50)
);
```

Here, `ID` is a unique identifier for each toy car, `Color` is the color of the car, `Size` is the size, `Brand` is the brand, and `Type` is the type of car.

And if we want to add a toy car to our table, we might use this SQL command:

```sql
INSERT INTO ToyCars (ID, Color, Size, Brand, Type) 
VALUES (1, 'Red', 'Small', 'Hot Wheels', 'Racing Car');
```

This is saying, "put a new toy car in the ToyCars box. Its ID is 1, its color is red, its size is small, its brand is Hot Wheels, and it's a racing car."

But why is it called a "relational" database? This is because the tables (or toy boxes) can be related to each other. For example, we might have another table called `ToyOwners` that keeps track of who owns which toy. This table might have a column that refers to the ID in `ToyCars`, showing who owns each car. This creates a 'relation' between the `ToyOwners` and `ToyCars` tables.

Here is how we can define the `ToyOwners` table:

```sql
CREATE TABLE ToyOwners (
    OwnerID INT PRIMARY KEY,
    Name VARCHAR(50),
    CarID INT,
    FOREIGN KEY (CarID) REFERENCES ToyCars(ID)
);
```

And to add a toy owner to the table, we might use this SQL command:

```sql
INSERT INTO ToyOwners (OwnerID, Name, CarID) 
VALUES (1, 'John', 1);
```

This is saying, "John, who has the OwnerID of 1, owns the toy car with an ID of 1."

### NoSQL

- Databases are primarily called as non-relational or distributed database.

Alright, let's continue our toys analogy to explain non-relational or distributed databases.

Remember how we organized your toys into boxes based on their type? Toy cars in one box, action figures in another, and so on? Each box had a strict rule about what type of toy could go in it, and each toy of the same type had the same characteristics: every car had a color, a size, a brand, etc.

Now, let's imagine a big toy chest where you can put any kind of toy, regardless of its type. You can put a toy car, an action figure, a puzzle, a teddy bear - anything you want. Each toy doesn't have to have the same characteristics; a teddy bear doesn't have a color in the same way a car does, and a puzzle doesn't have a brand like an action figure might. This is the basic idea of a non-relational database. You can store different types of data, and each piece of data doesn't have to follow the same structure.

A popular type of non-relational database is a document-oriented database. Each toy in our toy chest can be seen as a 'document'. Here's how you might define a toy car and a teddy bear in a document-oriented database like MongoDB:

```javascript
let toyCar = {
    type: "car",
    color: "red",
    size: "small",
    brand: "Hot Wheels"
};

let teddyBear = {
    type: "teddy bear",
    color: "brown",
    height: "large",
    name: "Teddy"
};

db.toys.insert(toyCar);
db.toys.insert(teddyBear);
```

In these JavaScript commands (MongoDB uses JavaScript), we first define the toy car and teddy bear, then we put them into our 'toys' collection, which is like our toy chest. Notice that the toy car and teddy bear don't have the same properties - that's fine in a non-relational database.

As for distributed databases, let's imagine that you have so many toys that they don't fit into one toy chest. You might put some of your toys in a toy chest at your house, some at your grandma's house, and some at your friend's house. Even though the toys are in different places, when you want to play, you could find and gather them from these different locations.

That's similar to how distributed databases work. Data is spread out across different computers, servers, or locations, but when you want to access the data, the database system brings it together so you can use it. This is good for handling very large amounts of data or for ensuring that the data is always available even if one location has a problem.

Most modern databases, both SQL (relational) and NoSQL (non-relational), can be set up to be distributed, including the MongoDB we've used in our examples.

### Different types of NoSQL databases

**1. Document-Based Databases**

Think of document databases like your school locker where you put all your different homework assignments. Each "document" is like a separate sheet of homework, and it can have all different kinds of information on it. Some sheets might be math homework, some sheets might be English homework, and so on. And just like your locker can have many different types of homework in it, a document database can have many different types of documents in it.

MongoDB is a type of document-based database. Here's how you might put a "document" (like a toy) into a MongoDB database:

```javascript
let toyCar = {
    type: "car",
    color: "red",
    size: "small",
    brand: "Hot Wheels"
};

db.toys.insert(toyCar);
```

**2. Key-Value Stores**

Key-value stores are like a big bunch of keys you might find at a hotel front desk. Each key (the 'key' in our database) has a tag with a room number on it, and that tag leads you to a room (the 'value' in our database). The 'room' can be anything you want it to be.

Redis is an example of a key-value store. Here's how you might store a 'key' and 'value' in Redis:

```shell
SET favoriteToy "Teddy Bear"
```

**3. Graph Databases**

Imagine you have a big family tree poster. It shows who is related to whom, who is the child of whom, who is the sibling of whom, and so on. Graph databases are like that family tree. They focus on the relationships between different pieces of data.

Neo4j is an example of a graph database. In Neo4j, you might store data like this:

```cypher
CREATE (Toy:Toy {name: "Teddy Bear"})<-[:OWNS]-(Owner:Owner {name: "John"})
```

This creates a toy named "Teddy Bear" and an owner named "John", and indicates that John owns the Teddy Bear.

**4. Wide-Column Stores**

Think of wide-column stores like a super-big spreadsheet. But unlike your typical spreadsheet, each row doesn't have to have the same number of columns, and different rows can have totally different kinds of information.

Cassandra is an example of a wide-column store. Here's how you might create a table and insert data in Cassandra:

```cql
CREATE TABLE Toys (
    ID UUID PRIMARY KEY,
    Name TEXT,
    Color TEXT,
    Brand TEXT
);

INSERT INTO Toys (ID, Name, Color, Brand) 
VALUES (uuid(), 'Hot Wheels', 'Red', 'Mattel');
```

That's a simplified overview of these NoSQL database types. They each have their own strengths, and the best one to use depends on what you need for your specific project.

### SQL Databases Have Predefined Schema, NoSQL Databases Have Dynamic Schema

This is like the difference between coloring in a coloring book (SQL) versus drawing your own picture on a blank sheet of paper (NoSQL). In the coloring book, you have to color inside the lines of the picture that's already there. But on a blank sheet of paper, you can draw anything you want.

### SQL Databases are Vertically Scalable, NoSQL Databases are Horizontally Scalable

Imagine you have a tower of blocks (like a database). If you want to make your tower taller (which is like making your database handle more data), you can do it in two ways:

- SQL databases are like adding bigger blocks underneath your tower to make it taller. This is called "vertical scaling" and it's like improving the hardware of a single computer running your database.

- NoSQL databases are like building more towers next to your original tower. This is called "horizontal scaling" and it's like adding more computers to your network to share the load of handling your data.

### SQL Uses SQL, NoSQL Uses Different Query Languages

This is like the difference between playing a game with a strict set of rules (SQL) versus a game where you can make up your own rules (NoSQL). In the SQL game, you have to use the structured query language (SQL), which is a powerful but strict set of rules for working with your data:

```sql
SELECT * FROM Toys WHERE Color = 'Red';
```

In the NoSQL game, you can use different types of commands, depending on what kind of game (or database) you're playing:

```javascript
// MongoDB
db.toys.find({color: "red"});
```

**SQL Database**

SQL databases are a good fit when you have structured and consistent data. They are beneficial when you need to maintain relationships between your data (like customers and their orders) and when you need complex queries and transactions to be consistent and reliable.

For instance, let's consider an online shopping website. It will have data like customer details, product details, order details, and shipping details. Each of these data sets have relationships with each other (like a customer can place multiple orders, each order can contain multiple products, etc.). SQL databases can handle this type of structured, relational data very well.

Here's an example of how you might create tables for this in an SQL database:

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(100),
    Email VARCHAR(100)
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

**NoSQL Database**

NoSQL databases are a good fit when your data is unstructured, flexible, or when you need to handle a large volume of data and scale horizontally.

For instance, consider a social media application like Twitter. It has data like user profiles, tweets, followers, and retweets. Some data, like tweets, may contain unstructured information like hashtags, @mentions, or attached images/videos. Also, data such as followers/following relationships can be easily modeled in graph-based NoSQL databases. The high volume of tweets and the need to scale horizontally also makes NoSQL a good fit.

Here's an example of how you might insert a tweet into a NoSQL database like MongoDB:

```javascript
let tweet = {
    username: "johnsmith",
    text: "Hello, world!",
    hashtags: ["#hello", "#world"],
    mentions: ["@friend1", "@friend2"],
    attached_images: ["image1.jpg", "image2.jpg"]
};

db.tweets.insert(tweet);
```

These are just examples, and the best type of database to use depends on your specific use-case, resources, and requirements.

**Hierarchical Data Storage**

For hierarchical data storage, graph databases (a type of NoSQL database) can be a great choice. Hierarchical data means there are clear relationships or dependencies from one piece of data to another, like a tree structure or a family lineage.

A graph database, like Neo4j, allows you to create nodes (entities) and edges (relationships), which makes it possible to easily model and traverse hierarchical data. You can think of a graph database as a big, interconnected web of data, where each piece of data can point directly to any other related piece of data.

For instance, in a family tree, each person could be a node and each parent-child relationship could be an edge. This kind of data is a perfect fit for a graph database.

Here's a simple example of how you might represent a parent-child relationship in Neo4j:

```cypher
CREATE (Parent:Person {name: "John"})-[:IS_PARENT_OF]->(Child:Person {name: "Alice"})
```

**Scalability**

When it comes to scalability, especially horizontal scalability (handling more data by adding more servers), NoSQL databases generally excel. NoSQL databases were designed to expand easily and they can handle large volumes of data or traffic.

Examples of such NoSQL databases include:

- **Cassandra**: A wide-column store that is highly scalable and designed to handle large amounts of data across many commodity servers, providing high availability with no single point of failure.

- **MongoDB**: A document-based database that supports sharding, allowing it to distribute data across multiple servers.

- **Couchbase**: A distributed, multi-model NoSQL document-oriented database that is optimized for interactive applications, providing low-latency data management for large-scale applications.

Remember, the "best" database often depends on the specific use-case, the nature of the data, and the resources available, so it's important to consider these factors when making a choice.

