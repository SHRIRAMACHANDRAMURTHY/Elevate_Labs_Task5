# Elevate_Labs_Task5
Joins, Relationships

1. Difference between INNER and LEFT JOIN

Definition:
An INNER JOIN returns only the rows that have matching values in both tables, while a LEFT JOIN returns all rows from the left table and the matching rows from the right table (if any).

Explanation in simple terms:

INNER JOIN: Keeps only the records that exist in both tables.

LEFT JOIN: Keeps all records from the left table, even if there’s no match in the right table. Non-matching rows from the right table appear as NULL.

Example:

SELECT e.EmployeeName, d.DepartmentName
FROM Employees e
INNER JOIN Departments d
ON e.DepartmentID = d.DepartmentID;


→ Only employees who belong to a valid department appear.

SELECT e.EmployeeName, d.DepartmentName
FROM Employees e
LEFT JOIN Departments d
ON e.DepartmentID = d.DepartmentID;


→ Shows all employees, even those not assigned to any department (DepartmentName will be NULL).

In short:
INNER JOIN → common rows only.
LEFT JOIN → all left table rows + matching right table rows.

2. What is a FULL OUTER JOIN?

Definition:
A FULL OUTER JOIN returns all rows from both tables, matching rows where possible, and filling NULL for missing matches.

Explanation:
It combines the results of LEFT JOIN and RIGHT JOIN. So, every record from both tables appears—whether it has a match or not.

Example:

SELECT e.EmployeeName, d.DepartmentName
FROM Employees e
FULL OUTER JOIN Departments d
ON e.DepartmentID = d.DepartmentID;


→ Includes all employees and all departments, showing NULLs where there’s no match.

In short:
FULL OUTER JOIN = LEFT JOIN + RIGHT JOIN combined.

3. Can joins be nested?

Answer:
Yes, joins can be nested — meaning you can join one table with another, and then join that result with yet another table.

Explanation:
You can chain multiple joins together or even use the result of one join as an input for another join.

Example:

SELECT e.EmployeeName, d.DepartmentName, l.LocationName
FROM (Employees e 
      INNER JOIN Departments d ON e.DepartmentID = d.DepartmentID)
INNER JOIN Locations l ON d.LocationID = l.LocationID;


→ This joins three tables step-by-step.

In short:
Yes, joins can be nested or chained to connect multiple tables in one query.

4. How to join more than 2 tables?

Explanation:
You can join more than two tables by chaining multiple JOIN clauses together, connecting each new table using its related keys.

Example:

SELECT e.EmployeeName, d.DepartmentName, l.LocationName
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DepartmentID
JOIN Locations l ON d.LocationID = l.LocationID;


→ Joins three tables: Employees → Departments → Locations.

In short:
Use multiple JOINs in one query to link 3 or more tables through their keys.

5. What is a CROSS JOIN?

Definition:
A CROSS JOIN returns the Cartesian product of two tables — every row in the first table combines with every row in the second table.

Explanation:
If Table A has 3 rows and Table B has 4 rows, a CROSS JOIN will return 3 × 4 = 12 rows.

Example:

SELECT a.StudentName, b.CourseName
FROM Students a
CROSS JOIN Courses b;


→ Lists all possible student–course combinations.

In short:
CROSS JOIN = all possible combinations between two tables.

6. What is a NATURAL JOIN?

Definition:
A NATURAL JOIN automatically joins two tables based on all columns with the same name and compatible data types.

Explanation:
You don’t have to specify the join condition explicitly; the database matches columns by name.

Example:

SELECT * 
FROM Employees 
NATURAL JOIN Departments;


→ Automatically joins where both tables have a column named DepartmentID.

In short:
NATURAL JOIN matches and joins using all columns with identical names.

7. Can you join tables without foreign key?

Answer:
Yes, you can.

Explanation:
A foreign key is not mandatory for performing a JOIN. You can join tables on any condition that logically relates the data — even if it’s not defined as a foreign key in the schema.

Example:

SELECT a.Name, b.City
FROM Customers a
JOIN Branches b 
ON a.Pincode = b.Pincode;


→ Joined using Pincode, not a foreign key.

In short:
You can join on any matching condition — a defined foreign key is not required.

8. What is a SELF JOIN?

Definition:
A SELF JOIN is when a table is joined with itself.

Explanation:
It’s useful for comparing rows within the same table — for example, finding employees who report to the same manager.

Example:

SELECT e1.EmployeeName AS Employee, e2.EmployeeName AS Manager
FROM Employees e1
JOIN Employees e2 ON e1.ManagerID = e2.EmployeeID;


→ Joins Employees table to itself to show employee–manager pairs.

In short:
SELF JOIN = joining a table to itself to compare related rows.

9. What causes a Cartesian product?

Answer:
A Cartesian product occurs when two tables are joined without a proper join condition (or with a CROSS JOIN).

Explanation:
Each row from the first table pairs with every row from the second, multiplying the number of rows drastically.

Example:

SELECT * FROM Employees, Departments;


→ Without an ON condition, it creates all possible combinations.

In short:
Missing or incorrect join condition = Cartesian product (all combinations).

10. How to optimize joins?

Answer:
Join optimization helps improve query speed and efficiency, especially with large tables.

Key techniques:

Use proper indexes on join columns (especially primary and foreign keys).

Join only necessary columns — avoid SELECT *.

Filter early using WHERE to reduce the dataset before joining.

Use appropriate join type (INNER JOIN is usually faster than OUTER JOIN).

Avoid unnecessary nested joins or complex subqueries.

Analyze execution plan to see which table should be joined first.

In short:
Use indexes, filter early, and keep joins minimal and relevant to improve performance.
