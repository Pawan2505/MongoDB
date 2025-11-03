
---

# **MongoDB – Projection**

---

### 🟢 **1. What is projection in MongoDB?**

**Answer:**
Projection in MongoDB is used to **control which fields** are returned in the query result.
It helps you include or exclude specific fields when retrieving documents using `.find()`.

---

### 🟢 **2. Why is projection useful?**

**Answer:**
Projection helps to:

* Reduce the amount of data transferred from the server.
* Improve query performance.
* Show only the required fields (useful for UI or reports).

---

### 🟢 **3. How do you include only specific fields in a query result?**

**Answer:**
You can specify the fields you want to include using `1` in the projection object.

**Example:**

```js
db.comments.find({}, { name: 1, lang: 1 })
```

👉 This shows only `name` and `lang` fields from all documents.
By default, `_id` is also included unless you exclude it explicitly.

---

### 🟢 **4. How do you exclude fields in projection?**

**Answer:**
Use `0` for fields you want to hide.

**Example:**

```js
db.comments.find({}, { lang: 0, member_since: 0 })
```

👉 This hides the `lang` and `member_since` fields and shows all others.

---

### 🟢 **5. Can you include and exclude fields together in projection?**

**Answer:**
No 
You **cannot mix inclusion and exclusion** in the same projection (except for `_id`).

**Example (Invalid):**

```js
db.comments.find({}, { name: 1, lang: 0 }) // Invalid
```

**Example (Valid):**

```js
db.comments.find({}, { name: 1, _id: 0 }) //  Valid
```

---

### 🟢 **6. How do you hide the `_id` field?**

**Answer:**
You can explicitly set `_id` to `0`.

**Example:**

```js
db.comments.find({}, { name: 1, lang: 1, _id: 0 })
```

👉 This shows only `name` and `lang`, and hides `_id`.

---

### 🟢 **7. Can you use projection with conditions in `.find()`?**

**Answer:**
Yes
You can combine a **query condition** with a **projection** in the same `.find()`.

**Example:**

```js
db.comments.find({ lang: "Python" }, { name: 1, member_since: 1, _id: 0 })
```

👉 Finds all comments where `lang` is "Python" and returns only the `name` and `member_since` fields.

---

### 🟢 **8. How can you use projection with nested fields?**

**Answer:**
You can use **dot notation** to project fields inside nested documents.

**Example:**

```js
db.users.find({}, { "profile.name": 1, "profile.email": 1, _id: 0 })
```

👉 Shows only the `name` and `email` inside the `profile` object.

---

### 🟢 **9. What happens if you don’t specify any projection?**

**Answer:**
MongoDB returns **all fields** by default.

**Example:**

```js
db.comments.find({ lang: "Python" })
```

👉 Returns full documents.

---

### 🟢 **10. Can projection improve performance?**

**Answer:**
Yes 
By fetching only required fields, projection **reduces data transfer** and speeds up queries, especially when documents have many fields.

---

### **Summary Table**

| Command                            | Description                  |
| ---------------------------------- | ---------------------------- |
| `{ field: 1 }`                     | Include specific field       |
| `{ field: 0 }`                     | Exclude specific field       |
| `{ _id: 0 }`                       | Exclude `_id` field          |
| Dot notation (`"profile.name": 1`) | Include nested field         |
| Mix inclusion and exclusion        | ❌ Not allowed (except `_id`) |

---

### **Recap**

```js
db.comments.find({}, { name: 1, lang: 1 })                // Include fields
db.comments.find({}, { lang: 0, member_since: 0 })        // Exclude fields
db.comments.find({ lang: "Python" }, { name: 1, _id: 0 }) // Condition + projection
db.users.find({}, { "profile.name": 1, _id: 0 })          // Nested projection
```

---

