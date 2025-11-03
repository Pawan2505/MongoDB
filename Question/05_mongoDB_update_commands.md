
---

## **MongoDB – Update Commands**

---

### 🟢 **1. How can you update one specific document in MongoDB?**

Use the command:

```js
db.comments.updateOne(
  { name: "Shubham" },
  { $set: { name: "Pawan", lang: "JavaScript", member_since: 51 } },
  { upsert: true }
)
```

**Explanation:**

* `{ name: "Shubham" }` → condition to find the document.
* `$set` → changes or adds the given fields.
* `{ upsert: true }` → if no document matches the condition, MongoDB will create a new one.

**Example:**
If Shubham’s record is found, it gets updated.
If not, a new record for Pawan will be added.

---

### 🟢 **2. How can you update multiple documents at once?**

Use:

```js
db.comments.updateMany(
  { lang: "JavaScript" },
  { $set: { verified: true } }
)
```

**Explanation:**
This will find **all** documents where `lang` is `"JavaScript"` and add a new field `verified: true` to each of them.

This is useful when you want to make the same change to many records.

---

### 🟢 **3. How can you increase (increment) a number field by a specific value?**

Use:

```js
db.comments.updateOne(
  { name: "Rohan" },
  { $inc: { member_since: 2 } }
)
```

**Explanation:**
The `$inc` operator increases a numeric field by the given number.
Here, Rohan’s `member_since` value will increase by `2`.

If the field doesn’t exist, MongoDB will create it and set it to the increment value.

---

### 🟢 **4. How can you rename a field in a document?**

Use:

```js
db.comments.updateOne(
  { name: "Rohan" },
  { $rename: { member_since: "member" } }
)
```

**Explanation:**
The `$rename` operator changes the field name from `member_since` to `member`.
This is useful if you want to change your data field names without losing data.

---

### 🟢 **5. What is the difference between `updateOne()` and `updateMany()`?**

| Command        | Description                                                     |
| -------------- | --------------------------------------------------------------- |
| `updateOne()`  | Updates only the **first** document that matches the condition. |
| `updateMany()` | Updates **all** documents that match the condition.             |

Example:
If 5 documents have `lang: "JavaScript"`,

* `updateOne()` changes only 1 of them.
* `updateMany()` changes all 5.

---

### 🟢 **6. What is the use of the `$set` operator in MongoDB?**

The `$set` operator is used to **add or update specific fields** in a document without changing the others.
Example:

```js
db.comments.updateOne(
  { name: "Fatima" },
  { $set: { lang: "Python" } }
)
```

This will only update the `lang` field, leaving other fields untouched.

---

### 🟢 **7. What is the `upsert` option in `updateOne()`?**

* `upsert: true` means:
  👉 *If a document doesn’t exist that matches the filter, MongoDB will insert a new one.*

Example:

```js
db.comments.updateOne(
  { name: "NewUser" },
  { $set: { lang: "C++", member_since: 1 } },
  { upsert: true }
)
```

If `NewUser` doesn’t exist, this command will create it.

---

### 🟢 **8. How can you decrease a numeric field value?**

You can use a **negative value** with `$inc`.
Example:

```js
db.comments.updateOne(
  { name: "Pawan" },
  { $inc: { member_since: -1 } }
)
```

This will reduce `member_since` by 1.

---

### 🟢 **9. How can you update multiple fields at once?**

Use `$set` with multiple key-value pairs:

```js
db.comments.updateOne(
  { name: "Pawan" },
  { $set: { lang: "Python", verified: true, level: "Pro" } }
)
```

This updates all three fields together.

---

### 🟢 **10. How can you remove a specific field from a document?**

Use the `$unset` operator:

```js
db.comments.updateOne(
  { name: "Pawan" },
  { $unset: { verified: "" } }
)
```

This removes the field `verified` from that document.

---

### **Summary:**

| Command        | Purpose                                 |
| -------------- | --------------------------------------- |
| `$set`         | Add or update specific fields           |
| `$inc`         | Increase or decrease a number           |
| `$rename`      | Rename a field                          |
| `$unset`       | Remove a field                          |
| `updateOne()`  | Update one document                     |
| `updateMany()` | Update multiple documents               |
| `upsert: true` | Create a new document if no match found |

---

### **Recap:**

```js
// Update one
db.comments.updateOne({ name: "Shubham" }, { $set: { lang: "JS" } })

// Update many
db.comments.updateMany({ lang: "JS" }, { $set: { verified: true } })

// Increment a number
db.comments.updateOne({ name: "Rohan" }, { $inc: { member_since: 2 } })

// Rename a field
db.comments.updateOne({ name: "Rohan" }, { $rename: { member_since: "member" } })
```

---

