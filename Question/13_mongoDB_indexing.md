
---

# **MongoDB – Indexing**

---

### 🟢 **1. What is an index in MongoDB?**

**Answer:**
An **index** in MongoDB is a **data structure** that improves the **speed of data retrieval** operations.
Without an index, MongoDB scans every document in a collection (called a **collection scan**) to find results — which is slow for large datasets.

👉 Think of an index like the index page in a book — it helps MongoDB quickly find the needed data.

---

### 🟢 **2. Why are indexes important?**

**Answer:**
Indexes help to:

* Speed up **search queries** (`find()`, `sort()`, etc.)
* Improve **query performance** on large collections
* Reduce the amount of data MongoDB scans

However, indexes slightly **slow down write operations** (insert, update, delete) because the index must also be updated.

---

### 🟢 **3. How do you create an index in MongoDB?**

**Answer:**

```js
db.comments.createIndex({ lang: 1 })
```

👉 Creates an **ascending index** on the `lang` field.
Use `-1` for **descending order**:

```js
db.comments.createIndex({ lang: -1 })
```

---

### 🟢 **4. What is the syntax for creating a compound index (on multiple fields)?**

**Answer:**

```js
db.comments.createIndex({ lang: 1, member_since: -1 })
```

👉 This index helps queries that filter or sort by both `lang` and `member_since`.
Compound indexes maintain the order of fields, so the sequence matters.

---

### 🟢 **5. How can you view all indexes in a collection?**

**Answer:**

```js
db.comments.getIndexes()
```

👉 Displays a list of all indexes created on the `comments` collection, including the default `_id` index.

---

### 🟢 **6. What is the default index in every MongoDB collection?**

**Answer:**
Every MongoDB collection automatically has a **default index** on the `_id` field.

```js
{ "_id": 1 }
```

👉 This ensures that each document is **unique** and can be retrieved quickly by its `_id`.

---

### 🟢 **7. How do you delete an index?**

**Answer:**

```js
db.comments.dropIndex({ lang: 1 })
```

👉 Drops the index on the `lang` field.

To drop **all indexes** (except `_id`):

```js
db.comments.dropIndexes()
```

---

### 🟢 **8. How can you check if a query is using an index?**

**Answer:**
Use the `.explain()` method.

**Example:**

```js
db.comments.find({ lang: "Python" }).explain("executionStats")
```

👉 If the result shows `"IXSCAN"`, it means the query used an index.
If it shows `"COLLSCAN"`, it scanned the entire collection.

---

### 🟢 **9. What are the types of indexes in MongoDB?**

| Index Type             | Description                     | Example                          |
| ---------------------- | ------------------------------- | -------------------------------- |
| **Single Field Index** | Index on one field              | `{ lang: 1 }`                    |
| **Compound Index**     | Index on multiple fields        | `{ lang: 1, member_since: -1 }`  |
| **Text Index**         | For text search                 | `{ name: "text", lang: "text" }` |
| **Hashed Index**       | For hashed sharding             | `{ user_id: "hashed" }`          |
| **Wildcard Index**     | Indexes all fields under a path | `{ "$**": 1 }`                   |

---

### 🟢 **10. What is a text index used for?**

**Answer:**
Text indexes are used for **full-text search** in string fields.

**Example:**

```js
db.comments.createIndex({ comment: "text" })
```

Then search using:

```js
db.comments.find({ $text: { $search: "mongodb" } })
```

👉 Returns documents containing the word **“mongodb”** in the `comment` field.

---

### 🟢 **11. What is a compound index and when should you use it?**

**Answer:**
A **compound index** includes multiple fields.
It’s useful when queries often use **more than one field** in filters or sorting.

**Example:**

```js
db.comments.createIndex({ lang: 1, member_since: -1 })
```

👉 Best used for queries like:

```js
db.comments.find({ lang: "Python" }).sort({ member_since: -1 })
```

---

### 🟢 **12. What is an index key pattern?**

**Answer:**
The **index key pattern** defines which fields are indexed and their sort order.

**Example:**

```js
{ lang: 1, member_since: -1 }
```

👉 Means ascending order for `lang` and descending order for `member_since`.

---

### 🟢 **13. What happens if you create the same index twice?**

**Answer:**
MongoDB will not create a duplicate index.
It checks the key pattern and ignores duplicate creation requests.

---

### 🟢 **14. What is the trade-off of using too many indexes?**

**Answer:**
Too many indexes can:

* Slow down write operations
* Use more disk space
* Increase maintenance overhead

Use indexes only on fields that are frequently **queried or sorted**.

---

### **Summary Table**

| Command                      | Description             |
| ---------------------------- | ----------------------- |
| `createIndex({ field: 1 })`  | Create an index         |
| `getIndexes()`               | View all indexes        |
| `dropIndex({ field: 1 })`    | Delete one index        |
| `dropIndexes()`              | Delete all indexes      |
| `.explain("executionStats")` | Check index usage       |
| `{ field: "text" }`          | Create a text index     |
| `{ "$**": 1 }`               | Create a wildcard index |

---

### **Recap**

```js
db.comments.createIndex({ lang: 1 })                    // Single field index
db.comments.createIndex({ lang: 1, member_since: -1 })  // Compound index
db.comments.getIndexes()                                // View indexes
db.comments.dropIndex({ lang: 1 })                      // Drop index
db.comments.find({ lang: "Python" }).explain("executionStats") // Check usage
db.comments.createIndex({ comment: "text" })            // Text index
```

---


