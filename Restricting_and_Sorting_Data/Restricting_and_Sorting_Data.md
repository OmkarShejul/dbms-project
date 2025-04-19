# Oracle SQL Notes

## Basic SELECT Statement
- **SELECT** specifies the columns to display.
- **FROM** specifies the table.

### Syntax
```sql
SELECT * FROM table_name;
SELECT column1, column2 FROM table_name;
```

![Basic SELECT Statement](https://www.sqltutorial.org/wp-content/uploads/2019/05/SQL-SELECT-Statement.png)

---

## SELECT Clause Enhancements
- **Column Aliases** using `AS` keyword or directly:
```sql
SELECT last_name AS name, salary AS income FROM employees;
SELECT last_name "Name", salary "Income" FROM employees;
```

- **String Literals**:
```sql
SELECT 'Employee Details' FROM dual;
```

- **Concatenation Operator (`||`)**:
```sql
SELECT first_name || ' ' || last_name AS full_name FROM employees;
```

- **Using Column Aliases with Expressions**:
```sql
SELECT salary + 1000 AS increased_salary FROM employees;
```

![SELECT Enhancements](https://www.geeksforgeeks.org/wp-content/uploads/SQL-Select-Clause.png)

---

## Display Structure of Table
```sql
DESC table_name;
```

---

## WHERE Clause
Used to filter rows.
```sql
SELECT * FROM employees WHERE department_id = 90;
```

![WHERE Clause](https://www.w3schools.com/sql/img_where.gif)

---

## NULL Values
- NULL represents missing or unknown data.
- NULL is **not** 0 or blank.
- Arithmetic operations with NULL result in NULL.

---

## DISTINCT Keyword
Eliminates duplicate rows.
```sql
SELECT DISTINCT department_id FROM employees;
```

![DISTINCT Keyword](https://www.w3schools.com/sql/img_distinct.gif)

---

## Combining Columns and Literals
```sql
SELECT first_name || ' works as ' || job_id AS job_info FROM employees;
```

---

## Practice Queries
1. Display employee ID, name, job ID, hire date:
```sql
SELECT employee_id, first_name || ' ' || last_name AS name, job_id, hire_date FROM employees;
```

2. Display names of employees in the HR department:
```sql
SELECT last_name FROM employees WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'HR');
```

3. Rename columns using aliases:
```sql
SELECT employee_id AS "Emp ID", first_name AS "First Name", job_id AS "Job", hire_date AS "Hire Date" FROM employees;
```

4. Concatenate first and last names:
```sql
SELECT employee_id, first_name || ', ' || last_name AS full_name FROM employees;
```

5. Display a custom label for department and manager:
```sql
SELECT department_name || ' Department''s Manager ID: ' || manager_id AS "Dept and Manager" FROM departments;
```

---

## Notes
- SQL is **not case-sensitive**.
- Statements can be on one or more lines.
- Always terminate SQL statements with a semicolon `;`.
- Use indentation and aliases to improve readability.

---

End of Notes.
