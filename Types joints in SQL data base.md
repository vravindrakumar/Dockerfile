In SQL, joins are used to combine rows from two or more tables based on a related column between them. There are several types of joins in SQL:

1. **Inner Join**
2. **Left Join (or Left Outer Join)**
3. **Right Join (or Right Outer Join)**
4. **Full Join (or Full Outer Join)**
5. **Cross Join**
6. **Self Join**


### 1. Inner Join
An **Inner Join** returns only the rows that have matching values in both tables. It is the most common type of join.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.common_column = table2.common_column;
```

**Example:**
```sql
SELECT employees.name, departments.name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.id;
```

### 2. Left Join (or Left Outer Join)
A **Left Join** returns all rows from the left table, and the matched rows from the right table. If no match is found, NULL values are returned for columns from the right table.

**Syntax:**
```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.common_column = table2.common_column;
```

**Example:**
```sql
SELECT employees.name, departments.name
FROM employees
LEFT JOIN departments
ON employees.department_id = departments.id;
```

### 3. Right Join (or Right Outer Join)
A **Right Join** returns all rows from the right table, and the matched rows from the left table. If no match is found, NULL values are returned for columns from the left table.

**Syntax:**
```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.common_column = table2.common_column;
```

**Example:**
```sql
SELECT employees.name, departments.name
FROM employees
RIGHT JOIN departments
ON employees.department_id = departments.id;
```

### 4. Full Join (or Full Outer Join)
A **Full Join** returns all rows when there is a match in one of the tables. If there is no match, the result is NULL on the side that does not have a match.

**Syntax:**
```sql
SELECT columns
FROM table1
FULL JOIN table2
ON table1.common_column = table2.common_column;
```

**Example:**
```sql
SELECT employees.name, departments.name
FROM employees
FULL JOIN departments
ON employees.department_id = departments.id;
```

### 5. Cross Join
A **Cross Join** returns the Cartesian product of the two tables, meaning it returns all possible combinations of rows from the tables.

**Syntax:**
```sql
SELECT columns
FROM table1
CROSS JOIN table2;
```

**Example:**
```sql
SELECT employees.name, departments.name
FROM employees
CROSS JOIN departments;
```

### 6. Self Join
A **Self Join** is a regular join but the table is joined with itself.

**Syntax:**
```sql
SELECT a.columns, b.columns
FROM table a, table b
WHERE condition;
```

**Example:**
```sql
SELECT a.name, b.name
FROM employees a, employees b
WHERE a.manager_id = b.id;
```
