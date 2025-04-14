
----
## 🧠 What is Normalization?
> **Normalization** is a process of organizing the data in the database to reduce **redundancy** and improve **data integrity**.

In simple words:
- It helps in **removing duplicate data**.
- It **splits large, unorganized tables** into smaller related ones.
- It **prevents anomalies** when inserting, deleting, or updating data.
---
## 🚨 Why is Normalization Needed?
Without normalization:
- Same data is repeated multiple times (data duplication).
- Inconsistencies can happen.
- You may update some copies of data and forget others.
- Inserting new data might require dummy values.
---
## 🔁 Types of Anomalies Normalization Fixes

| Type      | What It Means                                           |
| --------- | ------------------------------------------------------- |
| Insertion | Can't insert data unless other data is present          |
| Deletion  | Deleting one data causes loss of another                |
| Update    | Updating one copy but forgetting others causes mismatch |

-----
## 🏛️ Normal Forms (1NF to 3NF)
We will go through:
- ✅ 1NF (First Normal Form)
- ✅ 2NF (Second Normal Form)
- ✅ 3NF (Third Normal Form)
Let's take an example of a student-course table.
----
### 🔹 Example: Unnormalized Table
| StudentID | Name  | Course     | Instructor    |
| --------- | ----- | ---------- | ------------- |
| 1         | Alice | DBMS, Java | Sharma, Gupta |
| 2         | Bob   | DBMS       | Sharma        |
Here, we have **multiple values in a single cell** (comma-separated).

---
## 🔸 1NF – First Normal Form
> ✅ Rule: Each cell must contain **only one value**.

**Fix**: Split multi-valued columns into multiple rows.

| StudentID | Name  | Course | Instructor |
| --------- | ----- | ------ | ---------- |
| 1         | Alice | DBMS   | Sharma     |
| 1         | Alice | JAVA   | Gupta      |
| 2         | Bob   | DBMS   | Sharma     |
📌 Now every column has atomic (single) values = **1NF achieved**

----
## 🔸 2NF – Second Normal Form
> ✅ Rules: It should be in **1NF** and every **non-key column should depend on the whole primary key**(no partial dependency).
### 🤔 What is Partial Dependency?
If a table has **composite primary key**(e.g., `StudentID + Course`) and a column depends only on one part of it -> **partial dependency** -> break it!

---
**Problem in above table**:
- `Name` depends only on `StudentID`, not on `Course`
-----
**Fix**: Break into 2 tables:

### 🎓 Student Table

| StudentID | Name  |
| --------- | ----- |
| 1         | Alice |
| 2         | Bob   |
### 📘 Course Table

| StudentID | Course | Instructor |
| --------- | ------ | ---------- |
| 1         | DBMS   | Sharma     |
| 1         | JAVA   | Gupta      |
| 2         | DBMS   | Sharma     |
📌 Now all non-key columns depend on the whole key = **2NF achieved**

-----
## 🔸 3NF – Third Normal Form
> ✅ Rule: It should be in 2NF **and** there should be **no transitive dependency**.

### 🤔 What is Transitive Dependency?
If Column A->B->C
But A is the primary key -> then B -> C is **transitive** and must be removed.

-----
**Problem in Course table**:
- Instructor depends on Course, not on StudentID
- But Course is not the primary key -> This is a **transitive dependency**.
-----
**Fix**: Create an Instructor table.
### 🎓 Student Table

| StudentID | Name  |
| --------- | ----- |
| 1         | Alice |
| 2         | Bob   |
### 📘 Enrollment Table

| StudentID | Course |
| --------- | ------ |
| 1         | DBMS   |
| 1         | JAVA   |
| 2         | DBMS   |
### 👨‍🏫 Instructor Table

| Course | Instructor |
| ------ | ---------- |
| DBMS   | Sharma     |
| JAVA   | Gupta      |
📌 No transitive dependency = **3NF achieved**

---
## ✅ Summary Table

| Normal Form |                   Rule                   |                     Fix                     |
| :---------: | :--------------------------------------: | :-----------------------------------------: |
|     1NF     | Atomic values only(no multivalued cells) |       Split multiple values into rows       |
|     2NF     |  No partial dependency on composite key  |        Separated dependent  columns         |
|     3NF     |         No transitive dependency         | Move indirectly dependant data to new table |

----
## 💼 Interview Questions

---

### 🟢 Basic Level

---

### 1. **What is normalization in DBMS?**

> It’s a process of organizing data to reduce redundancy and avoid anomalies by dividing large tables into smaller ones.

---

### 2. **What problems does normalization solve?**

- **Redundancy (duplicate data)**
- **Anomalies**:
    - Insertion anomaly
    - Deletion anomaly
    - Update anomaly

---

### 3. **What is the difference between 1NF, 2NF, and 3NF?**

|Normal Form|Main Idea|
|---|---|
|1NF|No multi-valued columns (atomic)|
|2NF|No partial dependency|
|3NF|No transitive dependency|

---

### 4. **What is a partial dependency?**

> When a non-prime column depends only on a part of a composite primary key (not the whole key).

---

### 5. **What is a transitive dependency?**

> When a non-key column depends on another non-key column, instead of directly on the primary key.

---

### 🟡 Intermediate Level

---

### 6. **Why is normalization important in relational databases?**

- Reduces storage usage
- Increases data consistency
- Makes updates and inserts more efficient
- Makes maintenance easier

---

### 7. **Can a table be in 1NF and 3NF at the same time?**

> No. A table must first be in 1NF → then 2NF → then 3NF. It's a step-by-step process.

---

### 8. **What is denormalization?**

> The opposite of normalization — combining tables to improve performance (used in analytics or read-heavy systems).

---

### 🔴 Advanced

---

### 9. **What is BCNF (Boyce-Codd Normal Form)? How is it different from 3NF?**
> BCNF is a stricter version of 3NF. In BCNF, every determinant must be a candidate key.

🧠 _Extra tip:_ BCNF ≈ 3NF when table has only one candidate key.

---

### 10. **Does normalization affect performance?**

> Yes:
- **Positively** for data consistency
- **Negatively** for performance in very complex queries (more joins)

---

## 📝 Practice Problems

---

### 🔹 Problem 1:

**You are given this table:**

|Roll|Name|Subject|Teacher|
|---|---|---|---|
|1|Ram|Math, English|Sharma, Verma|

**Q:** Is this in 1NF? If not, normalize it
✅ **Answer**: No. Split multi-values into separate rows to achieve 1NF.

---

### 🔹 Problem 2:

**Given this table (already in 1NF):**

|EmpID|EmpName|DeptID|DeptName|
|---|---|---|---|
|101|John|10|HR|
|102|Alice|20|IT|
|103|Mark|10|HR|

**Q:** Is this table in 2NF and 3NF?
✅ **Answer**:

- 2NF: Yes (single primary key `EmpID`)
- 3NF: ❌ No. `DeptName` depends on `DeptID`, not directly on `EmpID`. So, move Dept info to separate table.