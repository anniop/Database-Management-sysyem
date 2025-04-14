---

---

---
## 🔗 What are JOINS in SQL?
When you  have **data in two or more tables** that is **related**, and you want to **combine** or **query** that data **together**, you use a **JOIN**.
### 🔍 In simple words:
> JOINS help you "connect the dots" between related data spread across different tables.
---
## 🤝 Real-Life Analogy
Imagine you have:
- 🧾 `Employees` table — stores names, age, salary, etc.
- 🏢 `Departments` table — stores department ID and department name
To find:
> What department does each employee work in?

You need to **JOIN** the two tables a **common column** (`dept_id`).

---
## 🧠 JOIN Terminology
- **Primary Key** - Unique identifier in one table (like `dept_id` in `Departments`).
- **Foreign Key** - Refers to the primary key of another table (like `dept_id` in `Employees`)
---
## 📘 Types of JOINS
---
### 🔸 1. INNER JOIN
**Keeps only matching rows** from both tables.
```sql
select *
from Employees
inner join Departments
on Employees.dept_id = Departments.dept_id;
```
✅ Result: Employees who are assigned to a department.  
❌ Excludes employees without a department or departments with no employees.

---
### 🔸 2. LEFT JOIN (LEFT OUTER JOIN)
**All rows from the left table(Employees)** and matching rows from the right table(Departments)
```sql
select *
from Employees
left join Departments
on Employees.dept_id = Departments.dept_id;
```
✅ Shows all employees — even those **without a department**  
📛 Department info will be `NULL` if unmatched

---
### 🔸 3. RIGHT JOIN (RIGHT OUTER JOIN)
**All rows from the right table(Departments)** and matching rows from the left table(Employees)
```sql
select *
from Employees
right join Departments
on Employees.dept_id = Departments.dept_id;
```
✅ Shows all departments — even those **without any employees**

---
### 🔸 4. FULL OUTER JOIN _(may not work in MySQL directly)_
Returns **all rows from both tables**, matched where possible, and `NULL` where not matched.
```sql
select *
from Employees
full outer join Departments
on Employees.dept_id = Departments.dept_id;
```
✅ Everyone and every department  
❌ Not supported natively in MySQL (but you can simulate it)

---
### 🛠️ Simulating `FULL OUTER JOIN` in MariaDB
```sql
select *
from Employees e
left join Departments d on e.dept_id = d.dept_id

union

select *
from employees e
right join Departments d on e.dept_id = d.dept_id;
```
#### 🧠 What This Does:
- The **first part**(LEFT JOIN) gets all employees, with department data if it exists.
- The **second  part**(RIGHT JOIN) gets all departments, even if they have no employees.
- `UNION` merges the two result sets, **removing duplicates** automatically.

#### ⚠️ Important Notes:
- Use `UNION ALL` instead of `UNION` if you want to **keep duplicates**(not recommended for full join logic).
- Make sure the **column order matches** in both queries (or else errors).
- This works fine for **most placement-level and interview queries**.

---
### 🔸 5. SELF JOIN
A table joined to itself
> _Find employees who report to the same manager._
```sql
select A.first_name, B.first_name
from Employees A, Employees B
where A.manager_id = B.id;
```
---
### 🔸 6. CROSS JOIN (a.k.a. Cartesian Product)
Every row in table A is matched with **every row** in table B.
```sql
select *
from Employees
cross join Departments;
```
😬 Be careful! A 10×10 table will return **100 rows**!

---
## 🧪 When to Use Which JOIN?

| Situtation                                     | JOIN to Use       |
| ---------------------------------------------- | ----------------- |
| You want only matching rows from both tables   | `INNER JOIN`      |
| You want all left-side rows, even if no match  | `LEFT JOIN`       |
| You want all right-side rows, even if no match | `RIGHT JOIN`      |
| You want all rows from both sides              | `FULL OUTER JOIN` |
| You want to compare rows in the same table     | `SELF JOIN`       |
| You want all combinations                      | `CROSS JOIN`      |

---
## ✅ Practice Questions (From Easy to Hard)
---
### 🟢 Easy
----
1. Show employee names with their department names(`INNER JOIN`)
	Answer:
```sql
select *
from Employees
inner join on Departments
on Employees.dept_id = Departments.dept_id;
```
---
2. Show all employees, even those without a department(`LEFT JOIN`)
	Answer:
```sql
select *
from Employees
left join on Departments
on Employees.dept_id = Departments.dept_id;
```
---
3. Show all departments, even those without employees(`RIGHT JOIN`)
	Answer:
```sql
select *
from Employees
right join on Departments
on Employees.dept_id = Departments.dept_id;
```
---
### 🟡 Medium
---
1. Show Departments along with the number of Employees in each department
    Answer:
```sql
select Departments.dept_id, Departments.dept_name, 
count(*) from Employees 
inner join Departments 
on Employees.dept_id = Departments.dept_id 
group by dept_name;
```
---
2. List employee names along with department name, and if no department, show "Not Assigned"
	Answer:
```sql
SELECT 
  e.first_name, 
  e.last_name, 
  COALESCE(d.dept_name, 'Not Assigned') AS department
FROM Employees e
LEFT JOIN Departments d ON e.dept_id = d.dept_id;
```
### 🧠 Explanation:
- `left join` -> keeps **all rows** from `Employees`, even if they have `NULL` in dept_id
- `COALESCE()` -> returns the first non-null value:
	- If `d.dept_name` is `NULL`, it shows `'Not Assigned'` instead.

---
### 🔴 Hard
---
1. Simulate `FULL OUTER JOIN`: show all employees and all departments, even if not linked.
	Answer:
```sql
select *
from Employees
left join Departments
on Employees.dept_id = Departments.dept_id

union

select * 
from Employees
right join Departments
on Employees.dept_id = Departments.dept_id;
```
---
2. Show departments with average salary of employees
	Answer:
```sql
select Departments.dept_name, avg(salary) 
from Employees 
left join Departments 
on Employees.dept_id = Departments.dept_id 
group by Departments.dept_name;
```
---
3. List departments where no employee is assigned
	Answer:
```sql
SELECT d.dept_name
FROM Departments d
LEFT JOIN Employees e ON d.dept_id = e.dept_id
WHERE e.dept_id IS NULL;
```
### 🧠 Explanation:

| Step                                           | What Happens                                                  |
| ---------------------------------------------- | ------------------------------------------------------------- |
| `LEFT JOIN`                                    | Keeps all departments, and brings matching employees (if any) |
| `WHERE e.dept_id IS NULL`                      | Filters only those departments with **no employees**          |

---
