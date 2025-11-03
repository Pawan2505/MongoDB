
---

## **MongoDB – Searching and Limiting Results**

---

### 🟢 **1. How can you find documents that match a specific field value?**

Use this command:

```js
db.comments.find({ lang: "Python" })
```

**Explanation:**
This shows all documents from the `comments` collection where the field `lang` is equal to `"Python"`.
It’s just like using a `WHERE` clause in SQL.

**Example Output:**

```js
{ _id: 1, lang: "Python", comment: "Easy to learn" }
{ _id: 3, lang: "Python", comment: "Used in AI" }
```

---

### 🟢 **2. How can you limit the number of results returned by a query?**

Use:

```js
db.comments.find().limit(2)
```

**Explanation:**
This command will show only the **first 2 documents** from the `comments` collection.
It’s useful when you don’t want to display too much data at once.

---

### 🟢 **3. What is the use of the `skip()` method in MongoDB?**

Use:

```js
db.comments.find().skip(2).limit(2)
```

**Explanation:**

* `skip(2)` → skips the first 2 documents.
* `limit(2)` → shows the next 2 documents after skipping.
  This is very useful for **pagination**, where you want to show data page by page.

**Example:**

* Page 1 → `skip(0).limit(2)`
* Page 2 → `skip(2).limit(2)`
* Page 3 → `skip(4).limit(2)`

---

### 🟢 **4. How can you count the total number of documents that match a condition?**

Use:

```js
db.comments.countDocuments({ lang: "Python" })
```

**Explanation:**
This command counts how many documents in the collection have `lang` set to `"Python"`.
It returns a number, for example:

```
2
```

---

### 🟢 **5. What’s the difference between `countDocuments()` and `estimatedDocumentCount()`?**

| Method                     | Description                                                                                                     |
| -------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `countDocuments()`         | Counts documents that match a given condition.                                                                  |
| `estimatedDocumentCount()` | Quickly estimates the total number of documents in the whole collection (faster but less accurate for filters). |

Example:

```js
db.comments.estimatedDocumentCount()
```

---

### 🟢 **6. How can you combine filter, limit, and skip together?**

Example:

```js
db.comments.find({ lang: "Python" }).skip(2).limit(3)
```

**Explanation:**
This will:

* Find only Python comments.
* Skip the first 2.
* Show the next 3.

---

### 🟢 **7. What happens if you use `limit()` without `find()`?**

You must always use `limit()` *after* a `find()` command.
For example:

```js
db.comments.limit(3)
```

❌ This won’t work correctly.
Use:

```js
db.comments.find().limit(3)
```

---

### **Summary:**

| Command                       | Description                     |
| ----------------------------- | ------------------------------- |
| `find({field: value})`        | Find documents with a condition |
| `limit(n)`                    | Limit the number of results     |
| `skip(n)`                     | Skip a number of results        |
| `countDocuments({condition})` | Count matching documents        |

---

### 📘 **Recap:**

```js
// Find all Python comments
db.comments.find({ lang: "Python" })

// Limit to first 2 results
db.comments.find().limit(2)

// Skip first 2 results and then show next 2
db.comments.find().skip(2).limit(2)

// Count how many Python comments exist
db.comments.countDocuments({ lang: "Python" })
```

---
