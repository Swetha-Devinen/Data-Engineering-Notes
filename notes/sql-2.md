1. Can a Table Have Number of Primary Keys?

A table can have only ONE Primary Key. That primary key can be made of multiple columns → called a Composite Primary Key
Syntax
PRIMARY KEY (column1, column2)

2. Aggregation

Aggregation functions perform calculations on multiple rows and return a single result.

Common Aggregate Functions

COUNT()

SUM()

AVG()

MIN()

MAX()

3. WHERE Condition / Clause: Used to filter rows based on a condition.

Syntax
SELECT column_name
FROM table_name
WHERE condition;

4. COUNT: Returns the number of rows.

Syntax
SELECT COUNT(column_name) FROM table_name;

5. DISTINCT: Returns unique values only.

Syntax
SELECT DISTINCT column_name FROM table_name;

6. LIMIT: Restricts the number of records returned.

Syntax
SELECT * FROM table_name LIMIT number;

7. Filtering with WHERE: Filters data based on conditions.

Example
SELECT * FROM employees WHERE salary > 50000;

8. Sorting – ORDER BY: Used to sort results.

Syntax
SELECT * FROM table_name ORDER BY column_name ASC;
SELECT * FROM table_name ORDER BY column_name DESC;

9. Operators in SQL
Logical Operators- AND, OR, NOT

Comparison Operators: = (equal), != or <> (not equal), <, >, <=, >=

Example
SELECT * FROM employees
WHERE salary > 40000 AND department = 'IT';

10. LIKE Operator: Used to search for patterns in a column.

Syntax
SELECT column_name
FROM table_name
WHERE column_name LIKE pattern;

11. Wildcards in SQL (Used with LIKE)

% - 	0, 1, or many characters
_ -	Exactly one character
LIKE Examples
Starts with A
SELECT city FROM sakila.city
WHERE city LIKE 'A%';

Ends with S
SELECT city FROM sakila.city
WHERE city LIKE '%S';

Contains 'AA' in second position
SELECT city FROM sakila.city
WHERE city LIKE '_AA%';

Exact single character match
SELECT city FROM sakila.city
WHERE city LIKE '_o%';

12. NULL: Checks for missing values.

Syntax
SELECT * FROM table_name WHERE column_name IS NULL;
SELECT * FROM table_name WHERE column_name IS NOT NULL;

13. BETWEEN: Used to filter values within a range.

Syntax
SELECT * FROM table_name
WHERE column_name BETWEEN value1 AND value2;

14. GROUP BY: Groups rows that have the same values.

Syntax
SELECT column_name, COUNT(*)
FROM table_name
GROUP BY column_name;

15. HAVING: Used to filter groups, not rows.

Syntax
SELECT column_name, COUNT(*)
FROM table_name
GROUP BY column_name
HAVING COUNT(*) > 5;

16. WHERE vs HAVING 
WHERE	Filters rows, Used before GROUP BY, Cannot use aggregate functions
HAVING Filters groups, Used after GROUP BY, Can use aggregate functions

17. Aliasing (AS): Used to rename columns temporarily.

Syntax
SELECT column_name AS alias_name FROM table_name;

18. Order of Execution in SQL

FROM

WHERE

GROUP BY

HAVING

SELECT

ORDER BY

LIMIT


