
---

# **MongoDB – Aggregation**

---

### 🟢 **1. What is aggregation in MongoDB?**

**Answer:**
Aggregation in MongoDB is a **powerful way to process and analyze data**.
It allows you to perform operations like filtering, grouping, sorting, counting, and calculating totals — similar to SQL’s `GROUP BY` and `SUM()`.

You use the `.aggregate()` method, which processes documents through **multiple stages**.

---

### 🟢 **2. What is the syntax of the aggregation pipeline?**

**Answer:**

```js
db.comments.aggregate([
  { stage1 },
  { stage2 },
  ...
])
```

Each stage takes input from the previous stage and transforms it.

**Example:**

```js
db.comments.aggregate([
  { $match: { lang: "Python" } },
  { $group: { _id: "$lang", totalUsers: { $sum: 1 } } }
])
```

---

### 🟢 **3. What are the most commonly used aggregation stages?**

| Stage      | Description                          |
| ---------- | ------------------------------------ |
| `$match`   | Filters documents (like `find`)      |
| `$group`   | Groups documents by a field          |
| `$sum`     | Adds numeric values                  |
| `$avg`     | Calculates the average               |
| `$sort`    | Sorts the results                    |
| `$project` | Selects or reshapes fields in output |

---

### 🟢 **4. What does `$match` do in aggregation?**

**Answer:**
`$match` filters documents based on a condition, just like a `find()` query.

**Example:**

```js
db.comments.aggregate([
  { $match: { lang: "Python" } }
])
```

👉 Filters only those documents where `lang` is `"Python"`.

---

### 🟢 **5. What does `$group` do in aggregation?**

**Answer:**
`$group` groups documents based on a field and allows you to perform operations like count, sum, or average.

**Example:**

```js
db.comments.aggregate([
  { $group: { _id: "$lang", totalMembers: { $sum: 1 } } }
])
```

👉 Groups comments by `lang` and counts how many belong to each language.

---

### 🟢 **6. How do you use `$sum` inside `$group`?**

**Answer:**
`$sum` adds up numeric values of a field.

**Example:**

```js
db.comments.aggregate([
  { $group: { _id: "$lang", totalMemberSince: { $sum: "$member_since" } } }
])
```

👉 For each language, it sums all `member_since` values.

---

### 🟢 **7. How does `$avg` work in aggregation?**

**Answer:**
`$avg` calculates the **average value** of a field across grouped documents.

**Example:**

```js
db.comments.aggregate([
  { $group: { _id: "$lang", avgMemberSince: { $avg: "$member_since" } } }
])
```

👉 Shows the average `member_since` value for each language.

---

### 🟢 **8. How do you sort aggregated results?**

**Answer:**
You can use `$sort` after grouping or matching.

**Example:**

```js
db.comments.aggregate([
  { $group: { _id: "$lang", totalUsers: { $sum: 1 } } },
  { $sort: { totalUsers: -1 } }
])
```

👉 Sorts the grouped results in **descending order** of total users.

---

### 🟢 **9. What does `$project` do in aggregation?**

**Answer:**
`$project` is used to include, exclude, or **rename fields** in the result.

**Example:**

```js
db.comments.aggregate([
  { $project: { name: 1, lang: 1, _id: 0 } }
])
```

👉 Displays only `name` and `lang`, hides `_id`.

---

### 🟢 **10. Can we use multiple stages together in one pipeline?**

**Answer:**
Yes ✅
You can combine multiple stages like `$match`, `$group`, `$sort`, and `$project` to create complex data processing pipelines.

**Example:**

```js
db.comments.aggregate([
  { $match: { lang: "JavaScript" } },
  { $group: { _id: "$lang", totalUsers: { $sum: 1 }, avgMemberSince: { $avg: "$member_since" } } },
  { $sort: { totalUsers: -1 } },
  { $project: { _id: 0, Language: "$_id", totalUsers: 1, avgMemberSince: 1 } }
])
```

👉 Filters JavaScript users, groups them, sorts by total, and then renames output fields.

---

### 🟢 **11. What is the difference between `.find()` and `.aggregate()`?**

| Feature               | `.find()`                 | `.aggregate()`               |
| --------------------- | ------------------------- | ---------------------------- |
| Purpose               | Retrieve data             | Process and analyze data     |
| Stages                | Single operation          | Multiple stages (pipeline)   |
| Grouping/Calculations | Not supported             | Supported                    |
| Performance           | Faster for simple queries | Better for complex analytics |

---

### **Summary Table**

| Operator   | Description        | Example                                            |
| ---------- | ------------------ | -------------------------------------------------- |
| `$match`   | Filters documents  | `{ $match: { lang: "Python" } }`                   |
| `$group`   | Groups documents   | `{ $group: { _id: "$lang", total: { $sum: 1 } } }` |
| `$sum`     | Adds numbers       | `{ $sum: "$field" }`                               |
| `$avg`     | Calculates average | `{ $avg: "$field" }`                               |
| `$sort`    | Sorts output       | `{ $sort: { field: 1 } }`                          |
| `$project` | Selects fields     | `{ $project: { name: 1, _id: 0 } }`                |

---

### **Recap**

```js
// Filter documents
db.comments.aggregate([{ $match: { lang: "Python" } }])

// Group by field
db.comments.aggregate([{ $group: { _id: "$lang", total: { $sum: 1 } } }])

// Average
db.comments.aggregate([{ $group: { _id: "$lang", avg: { $avg: "$member_since" } } }])

// Sort
db.comments.aggregate([{ $sort: { totalUsers: -1 } }])

// Full pipeline example
db.comments.aggregate([
  { $match: { lang: "JavaScript" } },
  { $group: { _id: "$lang", totalUsers: { $sum: 1 } } },
  { $sort: { totalUsers: -1 } },
  { $project: { Language: "$_id", totalUsers: 1, _id: 0 } }
])
```

---

