
---

## **MongoDB – Collection Commands**

---

### 🟢 **1. What is a collection in MongoDB?**

A collection in MongoDB is just like a **table** in SQL.
It stores a group of **documents** (records).
The good thing is that it doesn’t need a fixed structure — every document can have different fields.

---

### 🟢 **2. How can you see all collections in the current database?**

You can use this command:

```js
show collections
```

This will list all the collections available in the current database.

---

### 🟢 **3. How do you create a new collection named "comments"?**

You can use:

```js
db.createCollection("comments")
```

This will create a new empty collection named **comments**.
But remember — MongoDB can also **auto-create** a collection when you insert your first document.

---

### 🟢 **4. What happens if you create a collection that already exists?**

If you try to create a collection that’s already there, MongoDB will give an error message saying:

```
Collection already exists.
```

---

### 🟢 **5. How can you delete a collection named "comments"?**

You can use this command:

```js
db.comments.drop()
```

It will delete the whole collection along with all its data.
Once dropped, the data can’t be recovered.

---

### 🟢 **6. What is the difference between `createCollection()` and inserting data directly?**

| Method                      | Description                                                            |
| --------------------------- | ---------------------------------------------------------------------- |
| `db.createCollection()`     | Creates a collection manually (even if it’s empty).                    |
| `db.collection.insertOne()` | Automatically creates the collection when you add your first document. |

Example:

```js
db.posts.insertOne({ title: "Hello MongoDB" })
```

If **posts** doesn’t exist, MongoDB will make it automatically.

---

### 🟢 **7. Can we add some extra options when creating a collection?**

Yes! You can make a **capped collection** (a fixed-size collection).
Example:

```js
db.createCollection("logs", { capped: true, size: 5000 })
```

* `capped: true` → means it has a fixed size
* `size: 5000` → size limit in bytes
  When it becomes full, it will automatically replace the old data with new data.

---

### 🟢 **8. What is a capped collection?**

A **capped collection** is a collection with a fixed size.
When it’s full, old documents are replaced by new ones.
It’s useful for things like **logs or real-time data**.

---

### 🟢 **9. How do you check if a collection already exists?**

You can use:

```js
db.getCollectionNames()
```

This will show a list of all collection names in the current database.

---

### 🟢 **10. How can you rename an existing collection?**

You can rename a collection like this:

```js
db.oldCollection.renameCollection("newCollection")
```

This will change the collection name.

---

### 🟢 **11. How do you delete all collections at once?**

If you want to remove all collections from a database, you can simply delete the database itself:

```js
db.dropDatabase()
```

This removes all the collections inside it.

---

### 🟢 **12. How do you check if a collection is capped or not?**

Use this command:

```js
db.collectionName.isCapped()
```

It will return `true` if it’s capped, otherwise `false`.

---

### 🟢 **13. What happens when you run `show collections` after dropping one?**

If you delete a collection using `db.comments.drop()` and then run:

```js
show collections
```

You will no longer see `comments` in the list.

---

### 🟢 **14. What is the difference between a collection and a table?**

| SQL (Relational) | MongoDB (NoSQL)        |
| ---------------- | ---------------------- |
| Table            | Collection             |
| Row              | Document               |
| Column           | Field                  |
| Fixed structure  | Flexible (schema-less) |

---

### 🟢 **15. How can you check if your collection was successfully deleted?**

After running `db.comments.drop()`, run:

```js
show collections
```

If `comments` is not listed, it means the collection has been deleted successfully.

---

### **Summary:**

| Command                          | Description                |
| -------------------------------- | -------------------------- |
| `show collections`               | Shows all collections      |
| `db.createCollection("name")`    | Creates a new collection   |
| `db.collection.drop()`           | Deletes a collection       |
| `db.old.renameCollection("new")` | Renames a collection       |
| `db.getCollectionNames()`        | Lists all collection names |

---

