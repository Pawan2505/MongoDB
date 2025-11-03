***

## MongoDB Interview

MongoDB is one of the most popular databases used in modern web development, especially in the MERN stack. Below are the key topics to prepare before any MongoDB interview.

***

### 1. MongoDB Basics

Start with the fundamentals. These questions test if you understand what MongoDB is and how it differs from traditional databases.

- **What is MongoDB?**  
  MongoDB is a NoSQL, document-based database. It stores data in a flexible format called BSON (Binary JSON).

- **SQL vs NoSQL**  
  In SQL databases, we have tables with fixed schemas. MongoDB (NoSQL) is schema-free, easier to scale horizontally, and lets you store nested or complex data easily.

- **Collections and Documents**  
  Collections are like tables, and documents are like rows in SQL. But MongoDB documents can have flexible structures.

- **Common Data Types**  
  MongoDB supports data types such as string, number, boolean, date, array, object, ObjectId, and null.

- **ObjectId**  
  Every document in MongoDB has a default `_id` field, which is a unique ObjectId containing timestamp information.

- **BSON**  
  BSON is a binary-encoded version of JSON, used by MongoDB for storing and retrieving data efficiently.

***

### 2. CRUD Operations (Core Practical Area)

CRUD means Create, Read, Update, Delete — the core of database operations. You’ll almost always be asked about these.

- **Insert Data**  
  `db.collection.insertOne()` or `db.collection.insertMany()`

- **Read Data**  
  `db.collection.find()` or `db.collection.findOne()`

- **Update Data**  
  `updateOne()`, `updateMany()`, `replaceOne()`

- **Delete Data**  
  `deleteOne()`, `deleteMany()`

- **Query Operators**  
  Operators like `$eq`, `$gt`, `$lt`, `$in`, `$ne`, `$and`, `$or` are used for filtering data.

***

### 3. Querying and Filtering

Interviewers love practical questions like “find all users with age greater than 25”.

- **Projection** – Choose specific fields: `{ name: 1, age: 1 }`  
- **Sorting** – Sort results: `.sort({ age: -1 })`  
- **Limit/Skip** – Restrict or skip results: `.limit(5).skip(2)`  
- **Regex** – Search text using patterns.  
- **Embedded Documents** – Access nested data using dot notation: `"address.city": "Surat"`  

***

### 4. Schema Design Concepts

Schema design is about how you organize and relate your data.

- **Embedding vs Referencing**  
  Embed data when one-to-few, reference when one-to-many or many-to-many.

- **Data Modeling**  
  Plan how your collections work together — for example, how to design models for blogs, users, and comments.

- **Denormalization**  
  Sometimes data is copied to reduce joins and make reads faster.

***

### 5. Relationships and populate()

If you use Mongoose in Node.js or the MERN stack, understanding relationships is important.

- **Referencing with ObjectId** – Use ObjectId to link documents between collections.  
- **populate()** – Fetch the related data automatically.  
  Example:  
  ```js
  Post.find().populate('author')
  ```
- **Nested Population** – You can also populate deeper levels like `populate('author.profile')`.

***

### 6. Indexing and Performance

Indexes make your database faster when searching for specific data.

- **What is an Index?**  
  It’s a special data structure that speeds up queries.

- **Create Index**  
  `db.collection.createIndex({ name: 1 })`

- **Compound and Text Indexes** – Combine multiple fields or enable text searching.

- **Explain Plan** – Check performance using `.explain("executionStats")`.

***

### 7. Aggregation Framework

Aggregation helps process and analyze data, similar to using SQL’s `GROUP BY`.

- **What is Aggregation?**  
  It processes data through multiple stages called a pipeline.

- **Common Stages:** `$match`, `$group`, `$project`, `$sort`, `$limit`, `$lookup`, `$unwind`

- **Example:**
  ```js
  db.orders.aggregate([
    { $match: { status: "delivered" } },
    { $group: { _id: "$customerId", total: { $sum: "$amount" } } }
  ])
  ```

- **$lookup** – Used to combine data from another collection (like SQL join).

***

### 8. Validation and Security

Security and validation questions show how well you can protect data.

- **Schema Validation** – Set field rules using JSON Schema.  
- **User Authentication** – Use MongoDB Atlas or local user setup.  
- **Role-Based Access Control (RBAC)** – Give users only the permissions they need.

***

### 9. MongoDB Atlas and Deployment

Understanding cloud deployment is a plus.

- **What is MongoDB Atlas?**  
  It’s a cloud-based service for hosting MongoDB databases.

- **Connection String:**  
  `mongodb+srv://username:password@cluster.mongodb.net/dbname`

- **Backup, Monitoring, and Scaling** – Tools for maintaining production databases.

***

### 10. Mongoose (For MERN Stack Developers)

If you’re working with Node.js, Mongoose is the go-to ODM (Object Data Modeling) library.

- **Define Schema and Model** – Create structure for your collections.  
- **Create and Use Documents** – Insert and query data easily.  
- **Middleware Hooks (pre/post)** – Run functions before or after saving documents.  
- **Validation** – Ensure data quality at the schema level.  
- **Populate()** – Fetch related data automatically.  
- **Virtuals and Methods** – Add calculated or custom fields to your data.

***