ACID stands for:
> **A**tomicity, **C**onsistency, **I**solation, **D**urability

These are the **4 key properties** that ensures **reliability, safety, and correctness** of database transaction especially in multi-user, concurrent environments.

---
## 📌 What is a Transaction?
A **transaction** is a **sequence of operations** performed as a single logical unit of work
Example:
```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;
UPDATE accounts SET balance = balance + 100 WHERE account_id = 2;
COMMIT;
```
If one query fails, the whole transaction must be rolled back, That's where ACID comes in.

---
## 🧠 Let's Dive into Each ACID Property:
---
## 🔸 1. **Atomicity** – _"All or Nothing"_
### 📖 Definition:
A transaction should either **complete fully** or **have no effect at all**.
### ✅ Why It’s Important:
If your power goes out or a statement fails in the middle of a transaction, you don't want the database to be left in an **inconsistent state**.
### 🧪 Example:
```sql
-- Transfer ₹100 from Aniket to Ganesh
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE name = 'Aniket';  ✅
UPDATE accounts SET balance = balance + 100 WHERE name = 'Ganesh';  ❌
COMMIT;
```
- Atomicity ensures that **both operations roll back** Ganesh doesn't get ₹100 and Aniket doesn't lose ₹100.
---
## 🔸 2. **Consistency** – _"Valid to Valid State"_
### 📖 Definition:
A transaction must **take the datebase from one valid state to another valid state** following all integrity rules.
### ✅ Why It’s Important:
After any transaction, the **rules of the database (constraints, keys, etc) must still hold true**.
### 🧪 Example:
If a student's `marks` column allows only values from 0-100:
```sql
UPDATE students SET marks = 130 WHERE id = 5; -- ❌ violates constraint
```
- A **consistent** system will **reject** this transaction.
---
## 🔸 3. **Isolation** – _"Transactions Don’t Interfere"_
### 📖 Definition:
Even if transactions are running at the same time, they must appear to run **in isolation** without interfering with each other.
### ✅ Why It’s Important:
Imagine two users booking the last movie ticket at the same time. Isolation prevents **race conditions** and **data conflicts**.
### 🧪 Example:
Two queries:
```sql
Transaction A: UPDATE stock SET quantity = quantity - 1 WHERE item_id = 10;
Transaction B: UPDATE stock SET quantity = quantity - 1 WHERE item_id = 10;
```
- If not isolated properly, both might reduce quantity incorrectly.
### 🔒 Isolation Levels:
- Read Uncommitted (lowest)
- Read Committed
- Repeatable Read
- Serializable (highest & slowest)
---
## 🔸 4. **Durability** – _"Once Done, Always Done"_
### 📖 Definition:
Once a transaction is **committed**, it is **permanently saved**, even if the system crashes.
### ✅ Why It’s Important:
Durability ensures that data is **not lost** due to power failure, crash, or restart.
### 🧪 Example:
```sql
UPDATE accounts SET balance = 1000 WHERE user_id = 101;
COMMIT;
```
- Even if the server crashes a second later, the updated balance should be there when it restarts.
---
## 🧾 Summary Table:

| Property    | What it Means            | Why it's important               |
| ----------- | ------------------------ | -------------------------------- |
| Atomicity   | All-or-nothing execution | Avoids partial changes           |
| Consistency | Follow DB rules          | DB remains valid                 |
| Isolation   | Run like it's alone      | Prevents race conditions         |
| Durability  | Changes are permanent    | Survives crash, reboot, failures |

---
## 💼 Interview Questions
---
### 🟢 Basic Level
---
1. What are ACID properties in DBMS?
	- ACID stands for Atomicity, Consistency, Isolation, Durability.
	- They ensures reliable processing of transactions.
---
2. What is Atomicity in database transactions?
	- It ensures that either **all operations in a transaction succeed** or **none of them do**.
_Tip: Use the example of transferring money between accounts_
----
3. What is the purpose of the Consistency property?
	- It ensures that transactions move the database from **one valid start to another**, maintaining all constraints and rules.
----
4. How does Isolation help in concurrent transactions?
	- It ensures that **concurrent transactions do not affect each other's results**, making it seem like they executed one after the other.
---
5. What is Durability and how is it maintained?
	- Durability guarantees that once a transaction is committed, it will **survive crashes or power failures**.
	- It's usually maintained using **transaction logs** and **disk storage**.
---
### 🟡 Intermediate Level
---
6. What could happen if Atomicity is not ensured?
	- A transaction might partially update data, leading to an **inconsistent database state**(e.g., money debited from one account but not credited to another).
---
7. Can you explain Isolation with a real-world example?
	- Think of **online ticket booking**: If two users try to book the last seat, Isolation ensures only one succeeds and the data doesn't get corrupted.
---
8. What are Isolation Levels in SQL?
	- `READ UNCOMMITTED`, `READ COMMITTED`, `REPEATABLE READ`, `SERIALIZABLE`
	- They define how much one transaction can **see** another's changes.
----
9. What are some problems Isolation prevents?
	- **Dirty Read** - Reading uncommitted changes.
	- **Non-repeatable Read** - Getting different results from the same query in the same transaction.
	- **Phantom Read** - A row appears/disappears during execution.
----
### 🔴 Advanced / Theoretical
---
10. How do databases ensure Durability after a system crash?
	- They use mechanisms like **Write-Ahead Logging (WAL)**, where changes are first written to a log file before being applied to the database.
----
11. Explain a scenario where Isolation causes performance issue.
	- When `SERIALIZABLE` isolation is used, it can cause **lock contention**, making transactions slower. That's why lower levels are often used for read-heavy systems.
-----
12. Is it always necessary to follow all four ACID properties strictly?
	- In traditional RDBMS: Yes.
	- But in some NoSQL systems, **Consistency or Isolation is relaxed** (CAP theorem), favoring performance or availability.