
---
## 🧠 What is a Key?
> A **Key** is an attribute (or set of attributes) used to **uniquely identify a record** in a table.

 Imagine every row in a table is a student, and you want to be able to **quickly and uniquely** identify each student that's where **keys** come in.

---
## 🔍 Why are Keys Important?
- Help in identifying each row **uniquely**.
- Establish **relationships** between tables (via foreign keys)
- Enforce **data integrity**
- Improve **query performance**

---
## 🗂️ Types of Keys in DBMS
We'll understand:
1. ✅ **Primary Key**
2. ✅ **Candidate Key**
3. ✅ **Super Key**
4. ✅ **Foreign Key**
5. ✅ **Composite Key**
6. ✅ **Alternate Key**
Let's go step-by-step ⬇️
---
## 🔹 1. **Primary Key**
> A column (or group of columns) that **uniquely identifies** each record in a table.

### ✅ Rules:
- Cannot be `NULL`
- Must be unique
- Only **one primary key** per table
### 🧪 Example:
```sql
CREATE TABLE Students (
	roll_no INT PRIMARY KEY,
	name VARCHAR(50),
	age INT
);
```
- `roll_no` is unique for each student -> ✅ Primary Key
---
## 🔹 2. **Candidate Key**
> A column (or set of columns) that **can qualify** as a primary key.

There can be **multiple candidate keys** in a table, but only **one is chosen** as the primary key.
### 💡 Example:

| emp_id | email         | phone      |
| ------ | ------------- | ---------- |
| 101    | abc@gmail.com | 1234567890 |
- `emp_id`, `email`, `phone` -> all are **candidate keys**
---
## 🔹 3. **Super Key**
> A **set of attributes** that uniquely identifies a row.

✅ A super key can have **extra columns**; uniqueness is the only requirement.

### Example:
- `emp_id` -> super key ✅
- `emp_id + email` -> also super key ✅(even though extra)
> Every **candidate key is a super key**, but not every super key is a candidate key.

---
## 🔹 4. **Foreign Key**

> A column in one table that **references** the **primary key** of another table.

✅ Used to maintain **relationships** between tables.

### 💡 Example:
```sql
CREATE TABLE Departments (
	dept_id INT PRIMARY KEY,
	dept_name VARCHAR(50)
);

CREATE TABLE Employees(
	emp_id INT PRIMARY KEY,
	emp_name VARCHAR(50),
	dept_id INT,
	FOREIGN KEY (dept_id) REFERENCES Departments(dept_id)
);
```
- `dept_id` in `Employees` is a **foreign key**

---

## 🔹 5. **Composite Key**
> A **primary key** made of **multiple columns**.

Used when **no single column is unique**, but a **combination is**.
### 💡 Example:
| student_id | course_id | marks |
| ---------- | --------- | ----- |
| 1          | 101       | 85    |
| 1          | 102       | 90    |
- `(student_id, courese_id)` together -> composite key

---
## 🔹 6. **Alternate Key**
> Candidate keys **not chosen** as the primary key are called **alternate keys**

🧠 Think of them as the "runners-up".

---
## 🔁 Summary Table

|Key Type|Description|
|---|---|
|Primary Key|Uniquely identifies records; only one per table|
|Candidate Key|Possible choices for primary key|
|Super Key|Any set that uniquely identifies a record|
|Foreign Key|Points to a primary key in another table|
|Composite Key|Primary key made of multiple columns|
|Alternate Key|Candidate keys not selected as primary key|

---
## 🔥 Real-World Analogy

| You Are...        | Key Type                          |
| ----------------- | --------------------------------- |
| Your Roll No      | Primary Key                       |
| Your Email        | Candidate Key                     |
| Your Name + Email | Super Key                         |
| Your Class ID     | Foreign Key (link to class table) |

---
## 💼 Interview Questions

---

### 🟢 Basic Level

---

### 1. **What is a key in DBMS?**

> A key is an attribute (or set of attributes) that is used to **uniquely identify a row** in a table.

---

### 2. **What is the difference between a Primary Key and a Unique Key?**

|Feature|Primary Key|Unique Key|
|---|---|---|
|Uniqueness|Must be unique|Must be unique|
|Null values|❌ Not allowed|✅ Allowed (once)|
|Count per table|Only one primary key|Can have multiple|

---

### 3. **What is a candidate key?**

> A candidate key is a column (or group of columns) that can **uniquely identify rows**.  
> Among all candidate keys, **one becomes the primary key**.

---

### 4. **What is an alternate key?**

> Candidate keys that are **not selected** as the primary key are called alternate keys.

---

### 5. **What is a composite key?**

> A composite key is a **primary key made up of more than one column**.

📌 Example:  
`(student_id, course_id)` together can uniquely identify a record in a marks table.

---

### 🟡 Intermediate Level

---

### 6. **What is the difference between a candidate key and a super key?**

|Candidate Key|Super Key|
|---|---|
|Minimal set|May contain extra attributes|
|All candidate keys are super keys|Not all super keys are candidate keys|

---

### 7. **Can a table have multiple primary keys?**

> ❌ No. A table can have **only one primary key**, but that key can be made of multiple columns (composite key).

---

### 8. **Can a foreign key reference a non-primary column?**

> ✅ Yes — a foreign key can reference a **unique key**, but most commonly it refers to a **primary key**.

---

### 9. **Can a foreign key be null?**

> ✅ Yes. If the relationship is optional (i.e., not every row must have a related record), the foreign key can be null.

---

### 10. **What happens if you delete a referenced row from a table that has a foreign key?**

> It depends on the constraint:

- `ON DELETE CASCADE` → deletes the child rows too
- `ON DELETE SET NULL` → sets the foreign key to NULL
- ❌ No constraint → throws an error if child rows exist

---

### 🔴 Advanced Level

---

### 11. **Can a table have a composite primary key and a separate unique key?**

> ✅ Yes. You can define a **composite primary key** and also define **one or more unique keys** on different columns.

---

### 12. **What is the role of keys in normalization?**

> Keys (especially **candidate keys**) are used to identify:

- Partial dependency (2NF)
- Transitive dependency (3NF)
- Functional dependency