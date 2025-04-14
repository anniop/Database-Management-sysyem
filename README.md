# 📚 SQL & DBMS Placement Notes

Welcome to my SQL and DBMS notes repository — a **comprehensive, beginner-friendly, and interview-oriented** collection of everything you need to crack placement questions on databases and structured query language (SQL).

> 📌 Built using my own practice database so that I can *learn-by-doing* and also revisit these concepts easily.

---
## 🚀 What's Inside?

This repository contains:
### ✅ Practical SQL Notes (with Queries & Explanations)
| Topic                        | Status |
| ---------------------------- | ------ |
| SELECT, WHERE, AND, OR, LIKE | ✅ Done |
| Aggregate Functions          | ✅ Done |
| GROUP BY & HAVING            | ✅ Done |
| JOINS (INNER, LEFT, RIGHT)   | ✅ Done |
| Subqueries                   | ✅ Done |


---
### 📘 DBMS Theory Notes
| Topic                     | Status |
| ------------------------- | ------ |
| ACID Properties           | ✅ Done |
| Normalization (1NF - 3NF) | ✅ Done |
| Transactions & Locking    | ✅ Done |
| Keys, Indexes, Views      | ✅ Done |

---
## 🏗️ Practice Database Schema

I’ve created my own `EmployeesDB` to practice queries hands-on.
### 👨‍💼 Employees Table
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
➡️ More tables like Departments, Projects will be added as we explore JOINS.

---
## 💻 Tools Used
- SQL Playground / MySQL CLI / SQLite
- Obsidian for notes ✍️
- GitHub to track my revision 📌

---
## 🤝 Let's Connect
If you find this useful or want to collaborate on a data/SQL-focused project, let’s connect:
🔗 [LinkedIn](https://linkedin.com/in/aniket-mogal)
📬 Drop me a message, happy to help and learn together!

