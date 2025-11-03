
---

## **MongoDB – Delete Commands**

---

### 🟢 **1. How can you delete a single document in MongoDB?**

Use:

```js
db.comments.deleteOne({ name: "Harry" })
```

**Explanation:**
This command deletes **only the first document** that matches the given condition.
If multiple documents match, only the first one will be deleted.

**Example:**
If there are 3 documents where `name: "Harry"`, only the **first one** will be removed.

---

### 🟢 **2. How can you delete multiple documents at once?**

Use:

```js
db.comments.deleteMany({ lang: "Java" })
```

**Explanation:**
This command deletes **all documents** that match the condition.
In this example, all comments where `lang` is `"Java"` will be deleted.

---

### 🟢 **3. How can you delete all documents from a collection without dropping it?**

Use:

```js
db.comments.deleteMany({})
```

**Explanation:**
Passing an **empty filter `{}`** deletes **every document** inside the collection,
but the collection itself remains — meaning you can still insert new documents afterward.

---

### 🟢 **4. What is the difference between `deleteOne()` and `deleteMany()`?**

| Command        | Description                                                     |
| -------------- | --------------------------------------------------------------- |
| `deleteOne()`  | Deletes **only the first** document that matches the condition. |
| `deleteMany()` | Deletes **all** documents that match the condition.             |

**Example:**

```js
db.comments.deleteOne({ lang: "Python" })  // deletes 1
db.comments.deleteMany({ lang: "Python" }) // deletes all
```

---

### 🟢 **5. What will happen if you pass an empty filter in `deleteMany()`?**

**Answer:**
All documents in the collection will be deleted.

**Example:**

```js
db.comments.deleteMany({})
```

**Result:**
The collection becomes empty, but it still exists in the database.

---

### 🟢 **6. How can you verify how many documents were deleted?**

**Answer:**
MongoDB returns a result object that includes the count of deleted documents.

**Example:**

```js
const result = db.comments.deleteMany({ lang: "Java" })
print(result.deletedCount)
```

**Output Example:**

```
3
```

This means 3 documents were deleted.

---

### 🟢 **7. How can you remove a collection completely?**

**Answer:**

```js
db.comments.drop()
```

**Explanation:**

* `drop()` deletes the entire collection **and** all its documents.
* Once dropped, the collection is permanently removed from the database.

---

### 🟢 **8. What happens if the delete condition doesn’t match any document?**

**Answer:**
MongoDB will not throw an error.
It will simply return:

```js
{ acknowledged: true, deletedCount: 0 }
```

This means the delete command worked, but no matching documents were found.

---

### **Summary**

| Command              | Description                                         |
| -------------------- | --------------------------------------------------- |
| `deleteOne(filter)`  | Deletes the first document that matches the filter. |
| `deleteMany(filter)` | Deletes all matching documents.                     |
| `deleteMany({})`     | Deletes all documents (keeps collection).           |
| `drop()`             | Deletes the entire collection.                      |

---

### **Recap**

```js
// Delete one document
db.comments.deleteOne({ name: "Harry" })

// Delete multiple documents
db.comments.deleteMany({ lang: "Java" })

// Delete all documents
db.comments.deleteMany({})

// Drop the entire collection
db.comments.drop()
```

---

