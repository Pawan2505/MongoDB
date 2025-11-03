
---

# **MongoDB – Relationships & Data Modeling**

---

### 🟢 **1. What is data modeling in MongoDB?**

**Answer:**
Data modeling in MongoDB means **organizing and structuring data** to fit how your application will store and access it.

👉 It defines **how documents relate to each other** — just like tables in SQL.

MongoDB supports **two main types** of relationships:

1. **Embedding (Denormalization)**
2. **Referencing (Normalization)**

---

### 🟢 **2. What is embedding in MongoDB?**

**Answer:**
**Embedding** means storing related data **inside the same document**.

**Example:**

```js
{
  _id: 1,
  name: "Pawan",
  comments: [
    { text: "Great post!", date: "2025-10-20" },
    { text: "Nice content!", date: "2025-11-01" }
  ]
}
```

👉 Here, comments are **embedded** inside the user document.

**Use it when:**

* Related data is small and rarely changes independently.
* You frequently need all the data together.

**Advantages:**
Fast read performance
Simple queries (no joins)

**Disadvantages:**
❌ Document size can grow too large
❌ Difficult to update nested arrays

---

### 🟢 **3. What is referencing in MongoDB?**

**Answer:**
**Referencing** means storing the relationship using **ObjectIDs** instead of embedding data directly.

**Example:**

```js
// users collection
{
  _id: ObjectId("1"),
  name: "Pawan"
}

// comments collection
{
  _id: ObjectId("101"),
  user_id: ObjectId("1"),
  text: "Great post!"
}
```

👉 Here, the `user_id` field refers to the `_id` in the `users` collection.

**Use it when:**

* Related data is large or changes often.
* You don’t always need to load all related data.

**Advantages:**
Better for large datasets
Easier to update individual collections

**Disadvantages:**
❌ Requires multiple queries or `$lookup` (join-like operation)

---

### 🟢 **4. What is `$lookup` in MongoDB?**

**Answer:**
`$lookup` is used in the **aggregation pipeline** to perform a **join** between two collections (like SQL `JOIN`).

**Example:**

```js
db.comments.aggregate([
  {
    $lookup: {
      from: "users",          // target collection
      localField: "user_id",  // field in comments
      foreignField: "_id",    // field in users
      as: "userDetails"       // name for joined data
    }
  }
])
```

👉 This joins each comment with its corresponding user information.

**Result Example:**

```js
{
  _id: 101,
  text: "Great post!",
  user_id: ObjectId("1"),
  userDetails: [
    { _id: 1, name: "Pawan" }
  ]
}
```

---

### 🟢 **5. What is the difference between Embedding and Referencing?**

| Feature         | Embedding                       | Referencing                                 |
| --------------- | ------------------------------- | ------------------------------------------- |
| **Data stored** | Inside parent document          | In separate collections                     |
| **Performance** | Faster reads                    | Slower reads                                |
| **Update**      | Harder to update nested data    | Easier to update related data               |
| **When to use** | Small, related data             | Large, shared, or frequently changing data  |
| **Example**     | User + comments in one document | User in one collection, comments in another |

---

### 🟢 **6. Can you combine embedding and referencing?**

**Answer:**
Yes!
In real-world projects, developers often **mix both**.
You can embed small data (like usernames) and reference large or complex data (like user profiles).

**Example:**

```js
{
  text: "Nice tutorial!",
  user: { _id: ObjectId("1"), name: "Pawan" },  // partially embedded
  post_id: ObjectId("555")                      // reference
}
```

---

### 🟢 **7. What are the advantages of using `$lookup`?**

**Answer:**
Allows you to combine data from multiple collections
Helps maintain normalization
Useful for analytics and reporting queries

**However:**
❌ `$lookup` can be **slow** on large datasets because it performs joins at query time.

---

### 🟢 **8. Can `$lookup` join more than two collections?**

**Answer:**
Yes, by **nesting multiple `$lookup`** stages in a single aggregation pipeline.

**Example:**

```js
db.orders.aggregate([
  { $lookup: { from: "customers", localField: "cust_id", foreignField: "_id", as: "customer" } },
  { $lookup: { from: "products", localField: "product_id", foreignField: "_id", as: "product" } }
])
```

👉 This joins three collections: `orders`, `customers`, and `products`.

---

### 🟢 **9. What is the difference between `$lookup` and `$unwind`?**

| Operator    | Purpose                                       |
| ----------- | --------------------------------------------- |
| **$lookup** | Joins data from another collection            |
| **$unwind** | Breaks an array field into separate documents |

**Example:**
If `$lookup` returns an array of user details,
`$unwind` can split them into separate records.

```js
{ $unwind: "$userDetails" }
```

---

### 🟢 **10. What is denormalization?**

**Answer:**
**Denormalization** means storing duplicate data to improve **read performance**.
It’s commonly used in MongoDB because it avoids expensive joins.

Example:
Instead of storing `user_id`, you might directly store the user’s name and email in each post.

---

### **Summary Table**

| Concept             | Description                            | Example                         |
| ------------------- | -------------------------------------- | ------------------------------- |
| **Embedding**       | Store related data inside one document | User with comments array        |
| **Referencing**     | Store related data separately          | User and comments linked via ID |
| **$lookup**         | Performs joins between collections     | Combine user + comments         |
| **$unwind**         | Splits array fields                    | Used after `$lookup`            |
| **Denormalization** | Duplicate data for faster reads        | Store name/email directly       |

---

### **Recap**

```js
// Embedding Example
db.users.insertOne({
  name: "Pawan",
  comments: [{ text: "Good!" }, { text: "Nice!" }]
})

// Referencing Example
db.users.insertOne({ _id: 1, name: "Pawan" })
db.comments.insertOne({ text: "Good!", user_id: 1 })

// Lookup Example
db.comments.aggregate([
  { $lookup: { from: "users", localField: "user_id", foreignField: "_id", as: "userDetails" } }
])
```

---

