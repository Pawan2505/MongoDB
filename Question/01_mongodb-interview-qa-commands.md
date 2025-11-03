
***

### 1. How can you view all available databases in MongoDB?

**Answer:**  
To see all databases, type the following command in your MongoDB shell:

```
show dbs
```
Copy and paste this command to list every database that has data. Remember, empty databases aren’t shown.

***

### 2. How do you create a new database or switch to an existing one?

**Answer:**  
To create a new database or use an existing one, enter:

```
use dbName
```
Replace `dbName` with your chosen name. Copy and paste the command to switch instantly. The database is only created when you add data.

***

### 3. How can you check which database you are currently using?

**Answer:**  
To check the current active database, use this command:

```
db
```
Copy and paste to see which database you are working in. It simply prints the name (like `test`).

***

### 4. How can you delete the current database in MongoDB?

**Answer:**  
To delete the database you’re currently using, first switch to the database, then run:

```
use testDB
db.dropDatabase()
```
Copy and paste these two commands (replace `testDB` with your database name). The database will be permanently deleted.

***

### 5. What happens if you create a new database but don’t insert any data?

**Answer:**  
If you run:

```
use newDB
show dbs
```
(Copy and paste these commands, replace `newDB` with your name.)  
The new database won’t show up until you store at least one collection with documents inside.

***

