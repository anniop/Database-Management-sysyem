
----
## 🧾 What is a Transaction?
> A **transaction** is a sequence of one or more SQL operations performed as a **single logical unit of work**.

If any part of the transaction fails, the **entire transaction is rolled back**, and the data base returns to its previous stable state.

-----
### 🧠 Real-World Analogy:
💸 Think of **banking**:
> Transfer ₹1000 from Account A to Account B:
> 	1. "Debit ₹1000 from A"
> 	2. "Credit ₹1000 to B"

These **two steps together** form a **transaction**. If step 2 fails, step 1 should also be cancelled.

----
## 🔐 Properties of a Transaction – (ACID Reminder)
| Property    | Meaning                                     |
| ----------- | ------------------------------------------- |
| Atomicity   | All steps succeed or none at all            |
| Consistency | Data must remain valid and follow all rules |
| Isolation   | Each transaction acts as if it's alone      |
| Durability  | Once committed, the result is permanent     |

---
## ✅ SQL Commands for Transactions

| Command                       | Use Case                                      |
| ----------------------------- | --------------------------------------------- |
| `BEGIN` / `START TRANSACTION` | Starts a transaction                          |
| `COMMIT`                      | Save all changes                              |
| `ROLLBACK`                    | Cancel all changes                            |
| `SAVEPOINT`                   | Creates a rollback point inside a transaction |
| `RELEASE SAVEPOINT`           | Deletes a savepoint                           |
| `ROLLBACK TO SAVEPOINT`       | Rollbacks only till a savepoint               |

-----
## 📘 Example: Basic Transaction

```sql
START TRANSACTION

UPDATE accounts SET balance = balance - 500 WHERE account_id = 1;
UPDATE accounts SET balance = balance + 500 WHERE account_id = 2;

COMMIT;
```
If any statement fails, use `ROLLBACK;` instead of `COMMIT`

---
## 🎯 SAVEPOINT Example

```sql
START TRANSACTION

INSERT INTO orders VALUES (1,'Phone')L
SAVEPOINT sp1;

INSERT INTO orders VALUES (2, 'TV');
ROLLBACK TO sp1 --Cancles only the second insert

COMMIT; -- Saves the first Insert
```
---
## 🔒 Isolation Levels (For Advanced Understanding)
They define **how much one transaction can see the other.**

| Level            | Description                                     |
| ---------------- | ----------------------------------------------- |
| READ UNCOMMITTED | Can read uncommitted changes (least safe)       |
| READ COMMITTED   | Can only read committed changes                 |
| REPEATABLE READ  | Same query gives same result within transaction |
| SERIALIZABLE     | Highest level, full isolation(slowest)          |

----
### 🔥 Problems prevented by isolation levels:
|Problem|Description|
|---|---|
|Dirty Read|Reading uncommitted changes|
|Non-repeatable Read|Re-reading gives different results|
|Phantom Read|New rows appear/disappear between queries|

---
## 💼 Interview Questions & Answers
---
### 🟢 Basic Level

---

### 1. **What is a transaction in DBMS?**

> A transaction is a **sequence of one or more SQL operations** that are executed as a **single logical unit**.  
> Either all the operations succeed, or none of them are applied.

---

### 2. **What are the properties of a transaction?**

✅ **ACID** properties:

- **Atomicity**
- **Consistency**
- **Isolation**
- **Durability**

---

### 3. **What is the difference between COMMIT and ROLLBACK?**

|Keyword|Meaning|
|---|---|
|`COMMIT`|Saves all changes permanently|
|`ROLLBACK`|Undoes all changes since the transaction started|

---

### 4. **What is a SAVEPOINT in SQL?**

> A **SAVEPOINT** is a named point within a transaction where you can **roll back** to **without cancelling the entire transaction**.

---

### 5. **What are common problems that can happen if transactions are not isolated properly?**

|Problem|Description|
|---|---|
|**Dirty Read**|Read uncommitted data|
|**Non-repeatable Read**|Same query gives different results|
|**Phantom Read**|New rows appear/disappear mid-transaction|

---

### 🟡 Intermediate Level

---

### 6. **Explain Atomicity with an example.**

> Transferring money: If you debit ₹1000 from A but fail to credit it to B, the entire operation should be canceled.

---

### 7. **Why is Isolation important in transactions?**

> It prevents **race conditions**, **inconsistent results**, and **data conflicts** when multiple users access the database at the same time.

---

### 8. **What are the different Isolation Levels in SQL?**

|Isolation Level|Description|
|---|---|
|`READ UNCOMMITTED`|Least safe – dirty reads allowed|
|`READ COMMITTED`|Only committed data can be read|
|`REPEATABLE READ`|Rows stay locked – no changes while reading|
|`SERIALIZABLE`|Highest isolation – strictest and slowest|

---

### 9. **What is a dirty read?**

> When a transaction **reads data modified by another uncommitted transaction** — the changes could later be rolled back.

---

### 🔴 Advanced

---

### 10. **Can we rollback a committed transaction?**

> ❌ No. Once a transaction is committed, it is **permanent** and **cannot be undone**.

---

### 11. **When would you use a SAVEPOINT?**

> When you want to rollback part of a transaction **without cancelling the whole thing**, especially in complex operations.

---

### 12. **What is the difference between Transaction and Procedure?**

|Concept|Transaction|Procedure|
|---|---|---|
|Purpose|Ensures data consistency|Reusable block of SQL code|
|Rollback?|Yes|Only if transaction used inside|
|Control Flow|No (only commit/rollback)|Yes (if-else, loops, etc.)|

----
