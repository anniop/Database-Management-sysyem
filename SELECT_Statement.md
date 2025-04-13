## ## 🔍 What is SELECT?
The `SELECT` statement is used to **retrieve data** from one or more tables.
It is the most commonly used SQL command in interviews.

---
##  🛠 Syntax:
```sql
SELECT column1, column2, ...
FROM table_name;
```
### 🔸 Example:
```sql
SELECT name, age
FROM Employees;
```
---
## 🧠 Important Notes
- Use `*` to select all columns
	-> `SELECT * from Employees;`
- Column order matters in output.
- Column names must match the table scheme
- SQL is **case-insensitive** (but uppercase is preferred for keywords)
---
## 🎯 Variations with SELECT
### 1. Select Constants:
```sql
SELECT 1 + 1
-- Output: 2
```
### 2. Rename Columns using Aliases:
```sql
SELECT name AS EmployeeName, age AS AgeInYears
FROM Employees;
```
### 3. Use Expressions:
```sql
SELECT name, salary, salary * 12 AS AnnualSalary
FROM Empolyees;
```
### 4. Concatenate Strings (MySQL)
```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM Employees;
```
---
## ✅ 2–3 Practice Queries
