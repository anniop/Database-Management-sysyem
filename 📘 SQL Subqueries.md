## 🔍 What is a Subquery?
A **subquery** is a query **inside another query**.
It helps you:
- Compare a value with the result of another query.
- Filter records using values from another table.
- Dynamically calculate something.
---
## 🧠 Why Use Subqueries?
Because sometimes a single query **isn't enough** to get the data you want. you need to **run another query**.

---
## 🎯 Syntax Overview
### 1. 🧊 **Single-row subquery**
Returns one value.
```sql
select * from Employees
where salary > (select avg(salary) from Employees);
```
---
### 2. 📦 **Multi-row subquery**
Return multiple values.
```sql
select * from Employees
where dept_id in(select dept_id from Departments);
```
---
### 3. 🔄 **Subquery in FROM clause (inline view)**
```sql
select dept_name, total
from (
	select dept_id, sum(salary) as total
	from Employees
	group by dept_id
) as dept_summary
join Departments d on d.dept_id = dept_summary.dept_id;
```
---
### 4. 🚪 **Subquery in SELECT clause**
```sql
select 
first_name,
(select dept_name from Departments where dept_id = Employees.dept_id) as Department
from Employees;
```
----
## 🧾 Subquery Placement Types
|Use in...|Example|
|---|---|
|`WHERE`|salary > (SELECT ...)|
|`IN`, `NOT IN`|dept_id IN (SELECT ...)|
|`FROM`|JOIN with subquery|
|`SELECT`|Nested column lookups|
|`EXISTS`|Filter if subquery returns rows|

---
## 🔁 Subquery vs JOIN
| Use Case                                       | Best Option    |
| ---------------------------------------------- | -------------- |
| Want to **combine** rows                       | Use `JOIN`     |
| Want to **filter** rows based on another table | Use `SUBQUERY` |
