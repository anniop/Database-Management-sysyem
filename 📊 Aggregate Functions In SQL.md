## 🔍 What are Aggregate Functions?
Aggregate functions perform a **calculation on a group of rows** and return a single value.
Used most commonly with:
- `SELECT` (to summarize data)
- `GROUP BY` (to summarize per group)
- `HAVING` ( to filter aggregate results)
---
## 📋 Common Aggregate Functions

| Function  | Description                         | Example Result     |
| --------- | ----------------------------------- | ------------------ |
| `COUNT()` | Number of Rows (or non-null values) | Total Employees    |
| `SUM()`   | Total sum of numeric column         | Total Salary       |
| `AVG()`   | Average value of numeric column     | Avg Age            |
| `MIN()`   | Smallest value in a column          | Earliest hire data |
| `MAX()`   | Largest value in a column           | Highest salary     |

---
## 🛠 Syntax
```sql
SELECT AGG_FUNC(column)
FROM table
[WHERE condition];
```
---
## 📌 Examples on Employees Table
### 1. Count total number of employees
```sql
select count(*) from Employees;
```
---
### 2. Count number of employees in Engineering
```sql
select count(*) from Employees
where department = 'Engineering';
```
---
### 3. Total Salary paid to all employees
```sql
select sum(salary) from Employees;
```
---
### 4. Average salary of Marketing employees
```sql
select sum(salary) from Employees 
where department = 'Marketing';
```
---
### 5. Find the highest and lowest salary
```sql
select max(salary), min(salary)
from Employees;
```
---
### 6. Earliest Joining Data
```sql
select min(hire_date) from Employees;
```
---
## 🧪 Practice Queries
1. Count Number of Employees older than 30.
	Answer:-
	```sql
select count(*) from Employees where age > 30;
```
---
2. Get total salary paid in HR department
	Answer:-
	```sql
	select sum(salary) from Employees where department = 'HR';
```
---
3. Find average age of all employees
	Answer:-
	```sql
	select avg(age) from Employees;
```
---
4. Display maximum and minimum age of employees
	Answer:-
	```sql
select max(age), min(age)
from Employees;
```
---
5. Find sum of salary of employees hired after 2020
	Answer:-
	```sql
	select sum(salary)
	from Employees
	where hire_date > '2020-12-31';
```
---
## 💡 Interview Tips
- `COUNT(*)` includes nulls, `COUNT(column)` skips nulls
- Aggregate functions **ignore NULL** values except `COUNT(*)`
- Can be combined with `GROUP BY` for category-wise totals
- You **can't use the name  you gave to a column(alias)** in the same `SELECT` statement **before it's fully calculated**.