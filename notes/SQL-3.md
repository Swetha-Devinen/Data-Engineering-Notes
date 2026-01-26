Day-5: Jan 23
Built-in functions are predefined SQL functions used to:
	•	Manipulate strings
	•	Work with numbers
	•	Handle dates & time
	•	Perform calculations and aggregations

String Functions

Padding Data

Padding means adding extra characters/spaces to make strings the same length (useful for reports).

LPAD() – Left padding
Adds characters to the left

SELECT LPAD('SQL', 6, '*');

RPAD() – Right padding
Adds characters to the right

SELECT RPAD('SQL', 6, '*');

Use case: formatting output, aligning columns.


SUBSTRING() / SUBSTR()

Extracts part of a string.

SELECT SUBSTRING('Database', 1, 4);
--SQL***

CONCAT()

Joins two or more strings.

SELECT CONCAT('Hello', ' ', 'SQL');
-- Hello SQL


REVERSE()

Reverses a string.

SELECT REVERSE('SQL');
-- LQS


LENGTH()

Returns number of characters.

SELECT LENGTH('Hello');
-- 5


LOCATE()

Finds position of a substring.

SELECT LOCATE('a', 'Database');
-- 2

 SUBSTRING_INDEX()

Extracts string before/after a delimiter.

SELECT SUBSTRING_INDEX('a-b-c', '-', 1);
-- a

 UPPER() / LOWER()

Change case.

SELECT UPPER('sql'), LOWER('SQL');


LEFT() / RIGHT()

Extract characters from left/right.

SELECT LEFT('Database', 4), RIGHT('Database', 4);


CASE Statement

Used for conditional logic (if-else).

SELECT 
CASE 
  WHEN marks >= 50 THEN 'Pass'
  ELSE 'Fail'
END AS result
FROM students;

REPLACE()

Replaces part of a string.

SELECT REPLACE('SQL Server', 'Server', 'DB');
-- SQL DB

REGEXP

Pattern matching (advanced LIKE).

SELECT * FROM users
WHERE email REGEXP '.*@gmail.com';

 Aggregate Functions (Math + Count)
 COUNT()

Counts rows.

SELECT COUNT(*) FROM employees;

SUM()

Adds values.

SELECT SUM(salary) FROM employees;

AVG()

Average value.

SELECT AVG(salary) FROM employees;

MIN() / MAX()

Find smallest/largest value.

SELECT MIN(salary), MAX(salary) FROM employees;


 Date & Time Functions
 NOW()

Current date & time.

SELECT NOW();
 DATEDIFF()

Difference between two dates.

SELECT DATEDIFF('2025-01-30', '2025-01-20');
-- 10


Random & Numeric Functions

RAND()

Generates random number.

SELECT RAND();

 POWER()

Raises power.

SELECT POWER(2, 3);
-- 8

 MOD()

Remainder after division.

SELECT MOD(10, 3);
-- 1
 CEIL() & FLOOR()

Rounds numbers.

SELECT CEIL(91.68);   -- 92
SELECT FLOOR(91.68);  -- 91

	•	CEIL → next highest value
	•	FLOOR → next lowest value


Casting (Type Conversion)

Converts one datatype to another.

SELECT CAST('123' AS INT);

SQL Query Execution Order (Very Important)

SQL does NOT execute in the order you write.

Actual order:
	1.	FROM
	2.	WHERE
	3.	GROUP BY
	4.	HAVING
	5.	SELECT
	6.	ORDER BY

That’s why aggregate functions don’t work in WHERE.

 