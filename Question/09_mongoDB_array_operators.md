
---

# **MongoDB – Array Operators**

---

### 🟢 **1. What are array operators in MongoDB?**

**Answer:**
Array operators are used to **query fields that contain arrays**.
They help you check whether an array contains specific values, matches certain conditions, or has a particular length.

**Common array operators:**

* `$in`
* `$nin`
* `$all`
* `$size`
* `$elemMatch`

---

### 🟢 **2. What does the `$in` operator do?**

**Answer:**
`$in` checks if a field’s value **matches any value in the given array**.

**Example:**

```js
db.comments.find({ lang: { $in: ["English", "Hindi"] } })
```

👉 Finds all comments where `lang` is either **English** or **Hindi**.

---

### 🟢 **3. What does the `$nin` operator do?**

**Answer:**
`$nin` is the opposite of `$in`.
It finds documents where the field’s value **does NOT match any value** in the given array.

**Example:**

```js
db.comments.find({ lang: { $nin: ["English", "Hindi"] } })
```

👉 Finds all comments where `lang` is **neither English nor Hindi**.

---

### 🟢 **4. What does the `$all` operator do?**

**Answer:**
`$all` checks whether an array **contains all the specified elements** (order doesn’t matter).

**Example:**

```js
db.comments.find({ tags: { $all: ["mongodb", "database"] } })
```

👉 Finds all comments that have **both “mongodb” and “database”** in the `tags` array.

---

### 🟢 **5. What does the `$size` operator do?**

**Answer:**
`$size` is used to **find arrays of a specific length**.

**Example:**

```js
db.comments.find({ tags: { $size: 3 } })
```

👉 Finds all documents where the `tags` array has exactly **3 elements**.

---

### 🟢 **6. What does the `$elemMatch` operator do?**

**Answer:**
`$elemMatch` is used when you need to **match multiple conditions on the same array element**.

**Example:**

```js
db.comments.find({
  replies: { $elemMatch: { likes: { $gt: 10 }, verified: true } }
})
```

👉 Finds all comments where **at least one reply** has `likes > 10` **and** `verified = true`.

---

### 🟢 **7. Can `$in` be used with arrays inside documents?**

**Answer:**
Yes
If a document’s field contains an array, `$in` will match **if any element** of that array matches.

**Example:**

```js
db.comments.find({ tags: { $in: ["mongodb"] } })
```

👉 Matches documents even if `tags` is `["mongodb", "js", "nosql"]`.

---

### 🟢 **8. How does `$all` differ from `$in`?**

| Operator | Purpose                   | Example                       | Description                           |
| -------- | ------------------------- | ----------------------------- | ------------------------------------- |
| `$in`    | Matches **any one** value | `{tags: {$in: ["js","db"]}}`  | Matches if **either** js or db exists |
| `$all`   | Matches **all** values    | `{tags: {$all: ["js","db"]}}` | Matches if **both** js and db exist   |

---

### 🟢 **9. Can you combine `$size` and `$elemMatch` in a single query?**

**Answer:**
Yes You can combine them using `$and`.

**Example:**

```js
db.comments.find({
  $and: [
    { tags: { $size: 3 } },
    { replies: { $elemMatch: { likes: { $gt: 10 } } } }
  ]
})
```

👉 Finds comments having **3 tags** and at least **one reply with likes > 10**.

---

### 🟢 **10. Can `$elemMatch` be used for nested arrays?**

**Answer:**
Yes
`$elemMatch` works on **nested arrays** and is used for **complex queries** where multiple conditions must match on the **same array element**.

---

### **Summary Table**

| Operator     | Purpose                            | Example                                     | Description                                 |
| ------------ | ---------------------------------- | ------------------------------------------- | ------------------------------------------- |
| `$in`        | Match any value                    | `{lang: {$in: ["English","Hindi"]}}`        | Matches if field has any listed value       |
| `$nin`       | Exclude specific values            | `{lang: {$nin: ["English"]}}`               | Matches if field doesn’t have listed values |
| `$all`       | Match all values in array          | `{tags: {$all: ["js","db"]}}`               | Matches if all specified values exist       |
| `$size`      | Match array length                 | `{tags: {$size: 3}}`                        | Matches if array has 3 items                |
| `$elemMatch` | Match multiple conditions in array | `{replies: {$elemMatch: {likes:{$gt:10}}}}` | Matches when one element meets conditions   |

---

### **Recap**

```js
db.comments.find({ lang: { $in: ["English", "Hindi"] } })          // $in
db.comments.find({ lang: { $nin: ["English", "Hindi"] } })         // $nin
db.comments.find({ tags: { $all: ["mongodb", "database"] } })      // $all
db.comments.find({ tags: { $size: 3 } })                           // $size
db.comments.find({ replies: { $elemMatch: { likes: { $gt: 10 } } } }) // $elemMatch
```

---

