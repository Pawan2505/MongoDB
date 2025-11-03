
---

# **MongoDB – Sorting**

---

### 🟢 **1. What is sorting in MongoDB?**

**Answer:**
Sorting in MongoDB means arranging the documents in a collection in a **specific order** — either **ascending** or **descending** — based on one or more fields.

It helps you organize query results to make them easier to analyze or display in the UI.

---

### 🟢 **2. How do you sort documents in MongoDB?**

**Answer:**
Use the `.sort()` method after `.find()`.

**Example:**

```js
db.comments.find().sort({ member_since: 1 })
```

👉 This arranges the documents in **ascending order** based on the `member_since` field.

---

### 🟢 **3. What does the value inside the sort method mean?**

**Answer:**

* `1` → Sorts in **ascending** order (smallest to largest).
* `-1` → Sorts in **descending** order (largest to smallest).

**Examples:**

```js
db.comments.find().sort({ member_since: 1 })   // Ascending
db.comments.find().sort({ member_since: -1 })  // Descending
```

---

### 🟢 **4. How can you sort by multiple fields?**

**Answer:**
You can specify more than one field inside `.sort()` — MongoDB will sort by the **first field**, and if two documents are equal, it sorts by the **next field**.

**Example:**

```js
db.comments.find().sort({ lang: 1, member_since: -1 })
```

👉 Sorts first by `lang` (ascending),
and if two documents have the same `lang`, it sorts them by `member_since` (descending).

---

### 🟢 **5. How do you sort text fields alphabetically?**

**Answer:**
Sorting on text fields works the same way as numbers.

**Example:**

```js
db.comments.find().sort({ name: 1 })
```

👉 Arranges documents alphabetically by `name` (A → Z).
Use `-1` for reverse order (Z → A).

---

### 🟢 **6. How can you combine sorting with limit or skip for pagination?**

**Answer:**
You can use `.sort()` with `.limit()` and `.skip()` for pagination.

**Example:**

```js
db.comments.find().sort({ member_since: -1 }).skip(2).limit(3)
```

👉 Skips the first 2 documents, then shows the **next 3**, sorted by `member_since` in descending order.

---

### 🟢 **7. Does sorting affect the original collection order?**

**Answer:**
No ❌
Sorting only affects the **query result**, not the actual order of documents stored in the database.

---

### 🟢 **8. Can you sort on a field that doesn’t exist in all documents?**

**Answer:**
Yes ✅
Documents that don’t have the specified field will appear **at the end** of the sorted list (for ascending order).

---

### 🟢 **9. Is sorting case-sensitive in MongoDB?**

**Answer:**
Yes, by default MongoDB sorting is **case-sensitive** — uppercase letters come before lowercase letters.
You can control this using **collations**.

**Example (case-insensitive sort):**

```js
db.comments.find().collation({ locale: "en" }).sort({ name: 1 })
```

---

### **Summary Table**

| Command                            | Description                    |
| ---------------------------------- | ------------------------------ |
| `.sort({ field: 1 })`              | Sorts ascending (A→Z / 0→9)    |
| `.sort({ field: -1 })`             | Sorts descending (Z→A / 9→0)   |
| `.sort({ field1: 1, field2: -1 })` | Sorts by multiple fields       |
| `.sort().skip().limit()`           | Used for pagination            |
| `.collation({ locale: "en" })`     | Makes sorting case-insensitive |

---

### **Recap**

```js
db.comments.find().sort({ member_since: 1 })    // Ascending
db.comments.find().sort({ member_since: -1 })   // Descending
db.comments.find().sort({ lang: 1, member_since: -1 }) // Multiple fields
db.comments.find().sort({ name: 1 }).collation({ locale: "en" }) // Case-insensitive
```

---

