### ✅ Step 1: Create the Database
```sql
CREATE DATABASE EmployeeDB;
USE EmployeeDB;
```
---
### ✅ Step 2: Create the Main Table – `Employees`

```sql
CREATE TABLE Employees (
	id INT PRIMARY KEY AUTO_INCREMENT,
	first_name VARCHAR(50),
	last_name VARCHAR(50),
	age INT,
	department VARCHAR(50),
	salary INT,
	hire_date DATE
);
```
----
### ✅ Step 3: Insert Sample Data
```sql 
INSERT INTO Employees (first_name, last_name, age, department, salary, hire_date) VALUES
('John', 'Doe', 28, 'Engineering', 60000, '2021-06-12'),
('Alice', 'Smith', 34, 'HR', 50000, '2019-03-15'),
('Bob', 'Brown', 25, 'Engineering', 55000, '2022-01-20'),
('Emma', 'Davis', 30, 'Marketing', 48000, '2020-11-01'),
('Chris', 'Miller', 45, 'Finance', 70000, '2015-07-23');
```
---
### ✅ Step 4: Verify the Table
```sql
SELECT * FROM Employees;
```
---
