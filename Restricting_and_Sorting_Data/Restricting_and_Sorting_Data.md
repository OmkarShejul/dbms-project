# Oracle SQL Notes

## Basic SELECT Statement
- **SELECT** specifies the columns to display.
- **FROM** specifies the table.

### Syntax
```sql
SELECT * FROM table_name;
SELECT column1, column2 FROM table_name;
```


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


---

## Displaying the Structure of a Table

To understand the schema of a table — including column names, data types, and null constraints — you can use several methods in Oracle SQL.

### 🧪 Method 1: `DESC` Command (SQL*Plus / SQLcl)
```sql
DESC employees;
```
Shows:
```
Name           Null?    Type
-------------- -------- -----------------
EMPLOYEE_ID    NOT NULL NUMBER(6)
FIRST_NAME              VARCHAR2(20)
LAST_NAME     NOT NULL  VARCHAR2(25)
EMAIL         NOT NULL  VARCHAR2(100)
HIRE_DATE     NOT NULL  DATE
```

> ✅ **Use when** working in terminal-based tools like SQL*Plus or SQLcl.

---

### 📊 Method 2: Querying Data Dictionary — `USER_TAB_COLUMNS`
```sql
SELECT 
    column_name, 
    data_type, 
    data_length, 
    nullable
FROM 
    user_tab_columns
WHERE 
    table_name = 'EMPLOYEES';
```

> 💡 Note: Table names are **usually uppercase** in Oracle metadata views.

---

### 📌 Diagram: Table Structure Example


This diagram illustrates a simplified structure of a table with columns, types, and key constraints — just like what you'd see in a `DESC` or `USER_TAB_COLUMNS` query.

---

### 🛠️ Other Related Data Dictionary Views
| View Name           | Description                                  |
|---------------------|----------------------------------------------|
| `ALL_TAB_COLUMNS`   | Info on all tables the user can access       |
| `DBA_TAB_COLUMNS`   | Info on all tables in the database (DBA only)|
| `USER_TAB_COLUMNS`  | Info on tables owned by the user             |




---

## Filtering Data with the WHERE Clause

The `WHERE` clause is used to filter records that meet a specific condition. It’s one of the most essential clauses in SQL for retrieving targeted data.

### 🔍 Syntax
```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

### ✅ Examples

#### 1. Simple Equality
```sql
SELECT * FROM employees
WHERE department_id = 90;
```

#### 2. Multiple Conditions with AND / OR
```sql
SELECT * FROM employees
WHERE department_id = 90 AND salary > 10000;
```

#### 3. Using BETWEEN
```sql
SELECT * FROM employees
WHERE hire_date BETWEEN '01-JAN-2020' AND '31-DEC-2020';
```

#### 4. Using IN
```sql
SELECT * FROM employees
WHERE department_id IN (10, 20, 30);
```

#### 5. Using LIKE (pattern matching)
```sql
SELECT * FROM employees
WHERE last_name LIKE 'S%';  -- Names starting with S
```

#### 6. Checking for NULL
```sql
SELECT * FROM employees
WHERE commission_pct IS NULL;
```

---

### 📌 Diagram: WHERE Clause Filtering Logic

This diagram shows how the `WHERE` clause filters rows based on a logical condition.

---

### 💡 Tips
- Text values in conditions must be in **single quotes**: `'HR'`, `'John'`
- Date values depend on your **NLS date format** (e.g., `'01-JAN-2023'`)
- Use **parentheses** to group conditions when using `AND`/`OR` to avoid logic errors



---



---

## Handling NULL Values in Oracle SQL

`NULL` in SQL represents **missing, unknown, or undefined** data. It is not equivalent to `0` (zero) or an empty string — it means "no value."

---

### 🔍 Key Concepts:
- **NULL ≠ 0**: Zero is a number; NULL is an absence of a value.
- **NULL ≠ ''**: An empty string is still a value; NULL is unknown.
- **Any arithmetic operation with NULL results in NULL**.

---

### ⚠️ Example: Arithmetic with NULL
```sql
SELECT salary + NULL AS result FROM employees;
-- Output: NULL
```

---

### ✅ Checking for NULL

#### Use `IS NULL` or `IS NOT NULL`
```sql
SELECT * FROM employees
WHERE commission_pct IS NULL;
```

```sql
SELECT * FROM employees
WHERE manager_id IS NOT NULL;
```

> ❌ Do **not** use `= NULL` or `!= NULL` — they will not work!

---

### 🛠️ Functions for NULL Handling

#### 1. `NVL(expr1, expr2)` — Replaces NULL with a value
```sql
SELECT NVL(commission_pct, 0) AS commission FROM employees;
```

#### 2. `NVL2(expr1, expr2, expr3)` — If expr1 is NOT NULL, returns expr2; else returns expr3
```sql
SELECT NVL2(commission_pct, 'Has Commission', 'No Commission') AS status FROM employees;
```

#### 3. `COALESCE(expr1, expr2, ..., exprN)` — Returns first non-NULL expression
```sql
SELECT COALESCE(phone_number, email, 'No contact info') FROM employees;
```

---

### 📌 Diagram: NULL Behavior

![NULL Concept Diagram](https://www.sqltutorial.org/wp-content/uploads/2016/04/sql-null.png)

This diagram shows the difference between NULL, 0, and empty strings, and how functions like `NVL` and `COALESCE` handle them.

---

### 💡 Tips
- Use `NVL` or `COALESCE` to ensure cleaner output and prevent issues in reports.
- Be cautious when using `NULL` in `WHERE`, `JOIN`, and `GROUP BY` clauses.
- Avoid logic like `= NULL` — always use `IS NULL`.



---

## DISTINCT Keyword
Eliminates duplicate rows.
```sql
SELECT DISTINCT department_id FROM employees;
```


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
