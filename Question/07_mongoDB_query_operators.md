
---

## **MongoDB – Query Operators (Comparison Operators)**

*(Interview Questions & Answers)*

---

### 🟢 **1. What are query operators in MongoDB?**

**Answer:**
Query operators are **special symbols** used in MongoDB queries to filter data based on specific conditions.
They help compare values, match patterns, or check for existence.

Example:

```js
db.comments.find({ member_since: { $gt: 50 } })
```

This finds all documents where `member_since` is **greater than 50**.

---

### 🟢 **2. What does the `$lt` operator do?**

**Answer:**
The `$lt` operator means **“less than”**.
It returns documents where the field value is **less than** the given number.

**Example:**

```js
db.comments.find({ member_since: { $lt: 90 } })
```

👉 Finds all comments where `member_since` is **less than 90**.

---

### 🟢 **3. What does the `$lte` operator do?**

**Answer:**
The `$lte` operator means **“less than or equal to”**.
It returns documents where the field value is **less than or equal to** the given number.

**Example:**

```js
db.comments.find({ member_since: { $lte: 90 } })
```

👉 Finds all comments where `member_since` is **90 or below**.

---

### 🟢 **4. What does the `$gt` operator do?**

**Answer:**
The `$gt` operator means **“greater than”**.
It returns documents where the field value is **greater than** the given number.

**Example:**

```js
db.comments.find({ member_since: { $gt: 90 } })
```

👉 Finds all comments where `member_since` is **more than 90**.

---

### 🟢 **5. What does the `$gte` operator do?**

**Answer:**
The `$gte` operator means **“greater than or equal to”**.
It returns documents where the field value is **greater than or equal to** the given number.

**Example:**

```js
db.comments.find({ member_since: { $gte: 90 } })
```

👉 Finds all comments where `member_since` is **90 or higher**.

---

### 🟢 **6. What does the `$ne` operator do?**

**Answer:**
The `$ne` operator means **“not equal to”**.
It returns documents where the field value **does not match** the given value.

**Example:**

```js
db.comments.find({ member_since: { $ne: 5 } })
```

👉 Finds all comments where `member_since` is **not equal to 5**.

---

### 🟢 **7. Can you combine multiple comparison operators in one query?**

**Answer:**
Yes
You can combine multiple comparison operators inside the same condition.

**Example:**

```js
db.comments.find({
  member_since: { $gte: 10, $lte: 100 }
})
```

👉 Finds all comments where `member_since` is **between 10 and 100**.

---

### 🟢 **8. What happens if a field does not exist in a document when using comparison operators?**

**Answer:**
If the field doesn’t exist, the document **will not match** the condition.
Example:

```js
db.comments.find({ age: { $gt: 30 } })
```

If a document doesn’t have an `age` field, it won’t be included in the results.

---

### 🟢 **9. How is `$ne` different from logical NOT?**

**Answer:**

* `$ne` checks if a **specific field’s value** is *not equal* to something.
* Logical NOT (`$not`) checks if a **whole condition** is not true.

**Example:**

```js
// Using $ne
db.comments.find({ lang: { $ne: "Python" } })

// Using $not
db.comments.find({ member_since: { $not: { $gte: 50 } } })
```

---

### **Summary Table**

| Operator | Meaning               | Example                      | Description                 |
| -------- | --------------------- | ---------------------------- | --------------------------- |
| `$lt`    | Less than             | `{member_since: {$lt: 90}}`  | Finds values less than 90   |
| `$lte`   | Less than or equal    | `{member_since: {$lte: 90}}` | Finds values 90 or below    |
| `$gt`    | Greater than          | `{member_since: {$gt: 90}}`  | Finds values more than 90   |
| `$gte`   | Greater than or equal | `{member_since: {$gte: 90}}` | Finds values 90 or above    |
| `$ne`    | Not equal             | `{member_since: {$ne: 5}}`   | Finds values not equal to 5 |

---

### **Recap**

```js
db.comments.find({ member_since: { $lt: 90 } })    // less than
db.comments.find({ member_since: { $lte: 90 } })   // less than or equal
db.comments.find({ member_since: { $gt: 90 } })    // greater than
db.comments.find({ member_since: { $gte: 90 } })   // greater than or equal
db.comments.find({ member_since: { $ne: 5 } })     // not equal
```

---
