
# Chapter 3 - SQL Queries and Reports

## Lab Experience

Creating the following reports required for AC Company:

### 1. Report for HR Department :
- **Requirement**: Display last name and salary of employees whose salary is greater than 2000.

```sql
SELECT last_name, salary
FROM employees
WHERE salary > 2000;
```

### 2. Details of Employee Number 495 :
- **Requirement**: Display all details for employee number 495.

```sql
SELECT *
FROM employees
WHERE employee_id = 495;
```

### 3. Employees with Salary NOT Between 5000 and 8000 :
- **Requirement**: Display last name and salary of employees whose salary is NOT between 5000 and 8000.

```sql
SELECT last_name, salary
FROM employees
WHERE salary NOT BETWEEN 5000 AND 8000;
```

### 4. Employees with Last Name Starting with 'S' :
- **Requirement**: Display last names of employees whose last name starts with 'S'.

```sql
SELECT last_name
FROM employees
WHERE last_name LIKE 'S%';
```

### 5. Sort Employee Details by Last Name :
- **Requirement**: Sort employees by last name in ascending order.

```sql
SELECT last_name
FROM employees
ORDER BY last_name ASC;
```

## Substitution Variables in SQL :

- **Substitution Variable**: Prompt the user to input a value.
- **Used In**: 
  - WHERE clause
  - ORDER BY clause
  - Column expressions
  - Table names

**Example**:

```sql
SELECT employee_id, last_name, department_id
FROM employees
WHERE employee_id = &employee_id;
```

## Notes on Substitution Variables :
- **Character and Date Values**: Must be enclosed in single quotes (`' '`).
- **Numeric Values**: Can be directly input.

### Example Query Using Substitution Variable

```sql
SELECT last_name, department_id, salary * 12
FROM employees
WHERE job_id = '&job_id';
```

## DEFINE Command in SQL
- **Purpose**: Create and assign a value to a variable.

### Example:

```sql
DEFINE dept_id = 10;
SELECT employee_id, last_name
FROM employees
WHERE department_id = &dept_id;
```

## ORDER BY Clause with Substitution Variable

```sql
SELECT employee_id, last_name
FROM employees
ORDER BY &column_name;
```

---

> **Note**: Always test your queries properly while using substitution variables to avoid SQL injection risks.
