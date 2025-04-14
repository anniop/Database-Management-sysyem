## 🔍 What is GROUP BY?
Imagine you have a big list of employees and you want to:
- Count how many employees are in each department.
- Or get the total salary per department.
- Or the average age of employees per team
**You group the data by some column(like department)** and then apply a **math function** to each group that's what `GROUP BY` does.
---
### 🧪 Real-Life Analogy:
You have a list of students with their marks. you want to find:
- The average marks **per subject**.
- The number of students **per grade**.
You'd group by `subject` or `grade` and then apply functions like `AVG()` or `COUNT()`.

----
## 🛠 Syntax
```sql
select column_name, AGG_FUNC(column)
from table
group by column_name;
```
---
### 🎯 Example 1: Count employees in each department
```sql
select department, count(*) as employee_count
from Employees
group by department;
```
💡 This groups all employees by their `department`, then counts how many are in each one.

----
### 🧠 Key Rules of GROUP BY
- Every column in the `SELECT` line(expect for aggregates) **must appear in GROUP BY**.
- Can group by **multiple columns**
- `WHERE` filters **before grouping**, `HAVING` filters **after grouping**.
---
### 🧪 Example 2: Total salary in each department
```sql
select department, sum(salary) as total_salary
from employees
group by department;
```
### 🧪 Example 3: Average age by department
```sql
select department, avg(age) as avg_age
from employees
group by department;
```
---
### 🧪 Example 4: Group by multiple columns (department + age)
```sql
select department, age, count(*) as count
from Employees
group by department, age;
```
---
## 🎯 Introducing HAVING
### 🔍 What is HAVING?
Once you group data using `GROUP BY`, you may want to **filter** those groups.
But we **can't use** `WHERE` to filter groups
That's why we use `HAVING`.

---
### 🤔 Rule to Remember:
- ✅ Use `WHERE` to filter **rows**.
- ✅ Use `HAVING` to filter **groups**

---
### 🧪 Example 5: Departments with more than 1 employee
```sql
SELECT department, COUNT(*) AS emp_count
FROM Employees
GROUP BY department
HAVING COUNT(*) > 1;
```
---
### 🧪 Example 6: Departments with total salary above 100000
```sql
select department, sum(salary) as total_salary
from Employees
group by department
having sum(salary) > 10000;
```
---
## 🔁 Summary Table:


| Clause     | Used For         | Filters What?                            | Comes Before/After? |
| ---------- | ---------------- | ---------------------------------------- | ------------------- |
| `WHERE`    | Rows             | Individual rows                          | Before `GROUP BY`   |
| `GROUP BY` | Grouping rows    | Creates groups                           | After `WHERE`       |
| `HAVING`   | Filtering groups | Entire groups(with aggregate conditions) | After `GROUP BY`    |


---
## 🧪 Practice Queries
1. Count number of employees in each department
	Answer:
```sql
	select department, count(*) as total_Employees
	from Employees
	group by department
```
---
2. Show total salary of each department where salary is over 60000.
	Answer:
```sql
select department, sum(salary) as total_salary
from employees
group by department
having sum(salary) > 600000
```
---
3. Display departments where average age is over 30.
	Answer:
```sql
select department avg(age)
from Employees
group by department
having avg(age) > 30;
```
---
4. Count employees hired after 2020, grouped by department
	Answer:
```sql
select department, count(*)
from Employees
where hire_date > '2020-31-12'
group by department;
```
---
5. Show departments where more than 1 employee and total salary above 90000
	Answer:
```sql
select department, count(*), sum(salary)
from Employees
group by department
having sum(salary) > 90000 and count(*) > 1;
```
---
## More Practice Questions 
---
### 🟢 Easy Level
1. Count number of employees in each department.
	Answer:
```sql
select department, count(*) as total_employees
from Employees
group by department;
```
---
2. Get total salary given by each department
	Answer:
```sql
select department, sum(salary) as total_salary
from Employees
group by department;
```
---
3. Show average age of employees in each department.
	Answer:
```sql
select department, avg(age) as Average_Age
from Employees 
group by department;
```
---
### 🟡 Medium Level
1. Show departments where average salary is more than 50,000
	Answer:
```sql
select department, avg(salary) as Average_Salary
from Employees
group by department
having avg(salary) > 50000;
```

---

2. Show departments that have more than 1 employee
	Answer:
```sql
select department, count(*) as num_of_employees
from Employees
group by department
having count(*) > 1;
```
---
3. Show total salary per department but only include those with at least 2 employees
    Answer:
```sql
select department, sum(salary) as total_salary 
from Employees 
group by department 
having count(*) >= 2;
```
---
### 🔴 Hard Level
1. Count Employees hired **after 2020**, grouped by department
	Answer:
```sql
select department, count(*)
from Employees
where hire_date > '2020-12-31'
group by department;
```
---
2. Show departments where **average age > 30** and **total salary > 60,000**.
	Answer:
```sql
select department, avg(age), sum(salary)
from Employees
group by department
having avg(age) > 30 and sum(salary) > 60000;
```
---
3. Show department names with **less than 3 employees** but **more than 1**.
	Answer:
```sql
select department, count(*)
from Employees
group by department
having count(*) < 3 and count(*) > 1;
```
---
