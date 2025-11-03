
---

## **MongoDB – Document Commands**

---

### 🟢 **1. What is a document in MongoDB?**

A **document** in MongoDB is just like a **record or row** in SQL.
It stores data in **key-value pairs** inside **curly braces `{}`** and uses **BSON** (Binary JSON) format.

Example:

```js
{ name: "Pawan", age: 25, city: "Surat" }
```

---

### 🟢 **2. How can you insert a single document into a collection?**

You can use the command:

```js
db.students.insertOne({ name: "Fatima", age: 22, course: "BCA" })
```

This adds one document to the `students` collection.
If the collection doesn’t exist, MongoDB will automatically create it.

---

### 🟢 **3. How do you insert multiple documents at once?**

Use:

```js
db.students.insertMany([
  { name: "Pawan", age: 25 },
  { name: "Mastur", age: 24 },
  { name: "Fatima", age: 22 }
])
```

This will insert all the given documents into the collection together.

---

### 🟢 **4. How can you view all documents in a collection?**

Use the command:

```js
db.students.find()
```

It shows all documents stored in the collection.
You can also format the output nicely by using:

```js
db.students.find().pretty()
```

---

### 🟢 **5. How can you view only one document?**

Use:

```js
db.students.findOne()
```

It shows only the **first** document that matches your query.

---

### 🟢 **6. How do you search for specific data in documents?**

You can use conditions inside `find()`.
Example:

```js
db.students.find({ age: 25 })
```

This will show all students whose age is 25.

---

### 🟢 **7. How can you update one document in MongoDB?**

Use:

```js
db.students.updateOne(
  { name: "Pawan" },
  { $set: { city: "Ahmedabad" } }
)
```

**Explanation:**

* The first part `{ name: "Pawan" }` is the condition.
* The `$set` operator changes the value of `city` to “Ahmedabad”.

---

### 🟢 **8. How do you update many documents at once?**

Use:

```js
db.students.updateMany(
  { course: "BCA" },
  { $set: { status: "Active" } }
)
```

This updates all documents where `course` is “BCA”.

---

### 🟢 **9. How can you replace a document completely?**

Use:

```js
db.students.replaceOne(
  { name: "Pawan" },
  { name: "Pawan Maurya", age: 25, city: "Surat" }
)
```

**Note:** This will remove all old fields and replace them with the new ones.

---

### 🟢 **10. How do you delete one document?**

Use:

```js
db.students.deleteOne({ name: "Fatima" })
```

It will remove the first document that matches the condition.

---

### 🟢 **11. How do you delete multiple documents?**

Use:

```js
db.students.deleteMany({ course: "BCA" })
```

This removes all documents where the `course` is “BCA”.

---

### 🟢 **12. How can you delete all documents from a collection without deleting the collection itself?**

Use:

```js
db.students.deleteMany({})
```

This removes all documents but keeps the collection.

---

### 🟢 **13. What is the difference between `remove()`, `deleteOne()`, and `deleteMany()`?**

| Command        | Description                                   |
| -------------- | --------------------------------------------- |
| `remove()`     | Older method to delete data (now deprecated). |
| `deleteOne()`  | Deletes only the first matching document.     |
| `deleteMany()` | Deletes all matching documents.               |

---

### 🟢 **14. How can you find specific fields only (projection)?**

Use:

```js
db.students.find({}, { name: 1, city: 1 })
```

It will show only `name` and `city` fields for all documents.

---

### 🟢 **15. How can you count the total number of documents in a collection?**

Use:

```js
db.students.countDocuments()
```

or

```js
db.students.find().count()
```

---

### **Summary:**

| Command            | Description               |
| ------------------ | ------------------------- |
| `insertOne()`      | Add one document          |
| `insertMany()`     | Add many documents        |
| `find()`           | Show all documents        |
| `findOne()`        | Show one document         |
| `updateOne()`      | Update one document       |
| `updateMany()`     | Update multiple documents |
| `replaceOne()`     | Replace entire document   |
| `deleteOne()`      | Delete one document       |
| `deleteMany()`     | Delete multiple documents |
| `countDocuments()` | Count total documents     |

---

