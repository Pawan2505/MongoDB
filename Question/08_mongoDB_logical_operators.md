
---

## **MongoDB – Logical Operators**

---

### 🟢 **1. What are logical operators in MongoDB?**

**Answer:**
Logical operators are used to **combine multiple conditions** in a query.
They help you find documents that match **more complex logic**, like *both conditions true*, *either one true*, or *not true*.

**Common logical operators:**

* `$and`
* `$or`
* `$not`
* `$nor`

---

### 🟢 **2. What is the `$and` operator used for?**

**Answer:**
`$and` returns documents that **match all the given conditions** — both (or all) must be true.

**Example:**

```js
db.comments.find({
  $and: [
    { lang: "Python" },
    { member_since: { $gt: 50 } }
  ]
})
```

👉 Finds all comments where `lang` is `"Python"` **and** `member_since` is **greater than 50**.

**Shortcut:**
You can also write this without `$and`:

```js
db.comments.find({ lang: "Python", member_since: { $gt: 50 } })
```

---

### 🟢 **3. What is the `$or` operator used for?**

**Answer:**
`$or` returns documents that **match at least one** of the given conditions.

**Example:**

```js
db.comments.find({
  $or: [
    { lang: "Python" },
    { member_since: { $lt: 20 } }
  ]
})
```

👉 Finds all comments where either:

* `lang` is `"Python"`, **or**
* `member_since` is less than 20.

---

### 🟢 **4. What is the `$not` operator used for?**

**Answer:**
`$not` returns documents that **do not match** a specified condition.
It’s basically the opposite of the condition you write inside it.

**Example:**

```js
db.comments.find({
  member_since: { $not: { $gte: 50 } }
})
```

👉 Finds all comments where `member_since` is **not greater than or equal to 50** (i.e., less than 50).

---

### 🟢 **5. What is the `$nor` operator used for?**

**Answer:**
`$nor` returns documents that **fail all** the given conditions —
meaning **none** of the conditions are true.

**Example:**

```js
db.comments.find({
  $nor: [
    { lang: "Python" },
    { member_since: { $gt: 80 } }
  ]
})
```

👉 Finds all comments where:

* `lang` is **not** `"Python"`, **and**
* `member_since` is **not greater than 80**.

---

### 🟢 **6. What is the difference between `$and` and `$or`?**

| Operator | Meaning                       | Example                                        | Result                                     |
| -------- | ----------------------------- | ---------------------------------------------- | ------------------------------------------ |
| `$and`   | All conditions must be true   | `{ $and: [ {lang: "JS"}, {verified: true} ] }` | Only matches documents where both are true |
| `$or`    | Any one condition can be true | `{ $or: [ {lang: "JS"}, {verified: true} ] }`  | Matches documents where either is true     |

---

### 🟢 **7. Can you mix comparison and logical operators in one query?**

**Answer:**
Yes ✅
You can use comparison operators inside logical operators for advanced filtering.

**Example:**

```js
db.comments.find({
  $and: [
    { lang: "JavaScript" },
    { member_since: { $gte: 50, $lte: 100 } }
  ]
})
```

👉 Finds all comments where `lang` is `"JavaScript"` and `member_since` is between **50 and 100**.

---

### 🟢 **8. What will happen if none of the `$or` conditions are true?**

**Answer:**
If no document matches any condition in `$or`, MongoDB simply returns **an empty result** — it doesn’t throw an error.

---

### 🟢 **9. What is a real-world example using `$and` and `$or` together?**

**Example:**

```js
db.comments.find({
  $and: [
    { verified: true },
    { $or: [ { lang: "Python" }, { lang: "JavaScript" } ] }
  ]
})
```

👉 Finds all **verified users** who use **Python** or **JavaScript**.

---

### 🟢 **10. How can you use `$not` to find users who are not verified?**

**Example:**

```js
db.comments.find({
  verified: { $not: { $eq: true } }
})
```

👉 Finds all comments where `verified` is **not true**.

---

### **Summary Table**

| Operator | Meaning                      | Example                          | Description                     |
| -------- | ---------------------------- | -------------------------------- | ------------------------------- |
| `$and`   | Match all conditions         | `{ $and: [ {a:1}, {b:2} ] }`     | Both must be true               |
| `$or`    | Match any condition          | `{ $or: [ {a:1}, {b:2} ] }`      | Either can be true              |
| `$not`   | Opposite of condition        | `{ age: { $not: { $gte:18 } } }` | Not greater than or equal to 18 |
| `$nor`   | Match none of the conditions | `{ $nor: [ {a:1}, {b:2} ] }`     | Both must be false              |

---

### **Recap**

```js
// $and example
db.comments.find({ $and: [ { lang: "Python" }, { member_since: { $gt: 50 } } ] })

// $or example
db.comments.find({ $or: [ { lang: "Python" }, { member_since: { $lt: 20 } } ] })

// $not example
db.comments.find({ member_since: { $not: { $gte: 50 } } })

// $nor example
db.comments.find({ $nor: [ { lang: "Python" }, { member_since: { $gt: 80 } } ] })
```

---
